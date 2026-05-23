# API Throttling and Rate Limiting

Django API Throttling -
https://www.django-rest-framework.org/api-guide/throttling/
https://www.geeksforgeeks.org/python/how-to-throttle-api-with-django-rest-framework/
Django Rate Limiting - 
https://django-ratelimit.readthedocs.io/en/stable/usage.html


The application-level throttling provided by REST framework is intended for implementing policies such as different business tiers and basic protections against service over-use.


Yes — you *can* use django-ratelimit with Django REST Framework, and many teams do. But whether it’s *recommended* depends on what kind of rate limiting you need.

## Short answer

* For standard API throttling in DRF → prefer DRF’s built-in throttling system.
* For endpoint-specific or custom logic → `django-ratelimit` is perfectly reasonable.
* For serious production abuse protection → use infrastructure-level rate limiting too (NGINX, Cloudflare, API Gateway, etc.).

---

## DRF’s built-in throttling (usually recommended first)

DRF already provides:

* `AnonRateThrottle`
* `UserRateThrottle`
* `ScopedRateThrottle`

Example:

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.UserRateThrottle",
        "rest_framework.throttling.AnonRateThrottle",
    ],
    "DEFAULT_THROTTLE_RATES": {
        "user": "1000/day",
        "anon": "100/day",
    },
}
```

Advantages:

* Integrated with DRF authentication
* Returns proper API throttling responses
* Easy per-view configuration
* Maintained specifically for DRF APIs

Best for:

* General API request limiting
* Authenticated vs anonymous limits
* Scoped API limits

---

## When `django-ratelimit` is useful

`django-ratelimit` shines when you want:

* Per-IP protection
* Login brute-force protection
* Custom keys
* Function/view-level rules
* Non-DRF Django views too

Example on a DRF view:

```python
from django_ratelimit.decorators import ratelimit
from rest_framework.views import APIView

class MyView(APIView):

    @ratelimit(key='ip', rate='10/m', block=True)
    def post(self, request):
        ...
```

Or with function-based DRF views:

```python
@api_view(["POST"])
@ratelimit(key='ip', rate='5/m', block=True)
def login(request):
    ...
```

---

## Important caveat

`django-ratelimit` was designed primarily for Django views, not DRF internals.

That means:

* DRF throttling integrates better with API exception handling
* You may need custom handling for JSON errors
* Decorator order matters
* Class-based DRF views can be awkward

So for *general API throttling*, DRF throttles are cleaner.

---

## Common production setup

A strong setup often looks like:

| Layer               | Tool                     |
| ------------------- | ------------------------ |
| Edge/CDN            | Cloudflare / API Gateway |
| Reverse proxy       | NGINX rate limiting      |
| API framework       | DRF throttling           |
| Sensitive endpoints | django-ratelimit         |

Example:

* DRF throttles for normal API quotas
* `django-ratelimit` on login/password reset endpoints
* Cloudflare for DDoS/bot protection

That combination is very common.

---

## Recommendation

For your DRF APIs:

### Use DRF throttling for:

* API-wide limits
* User quotas
* Authenticated rate control

### Use `django-ratelimit` for:

* Login endpoints
* OTP endpoints
* Password reset abuse
* Extra IP-based blocking
* Hybrid Django + DRF apps

So:

* **Yes, it works**
* **Yes, it can be recommended**
* But usually **as a complement to DRF throttling, not a replacement**.



