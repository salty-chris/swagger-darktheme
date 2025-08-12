Swagger Dark Theme
==================

Dark mode CSS for Swagger UI — because API docs shouldn’t burn your eyeballs.

<img width="360" height="244" alt="image" src="https://github.com/user-attachments/assets/ca968ac1-df17-437b-9662-b6af2c281d89" />


Compatibility
-------------

- Tested with **OpenAPI 3.1**
- Designed for **FastAPI** + Swagger UI


Quick Start (FastAPI)
---------------------

1. Place ``swagger-dark.css`` in a ``/static`` folder at your project root
Sample placement:
```
       your-project/
       ├─ main.py
       └─ static/
          └─ swagger-dark.css
```

2. Mount static, disable the default docs, and serve a custom dark-themed page.
Example:

```
   from fastapi import FastAPI
   from fastapi.staticfiles import StaticFiles
   from fastapi.openapi.docs import get_swagger_ui_html

   app = FastAPI(
       docs_url=None,   # disable default /docs
       redoc_url=None,
       title="Your API Docs Title",
       description="Some description",
       swagger_ui_parameters={
           "defaultModelsExpandDepth": -1,  # hide models list
           "defaultModelExpandDepth": 0,    # collapse schemas by default
       },
   )

   # Serve static assets (CSS)
   app.mount("/static", StaticFiles(directory="static"), name="static")

   # Custom dark-themed Swagger UI
   @app.get("/docs", include_in_schema=False)
   async def custom_swagger_ui_html():
       return get_swagger_ui_html(
           openapi_url=app.openapi_url,
           title="API Docs — Salty Dark Theme",
           swagger_css_url="/static/swagger-dark.css",
       )
```
*tip*: Keep the route as `/docs` to match muscle memory, or rename it if you prefer.


Notes
-----

- Adjust `swagger_ui_parameters` to taste (expand/collapse behavior).
- The theme is CSS-only; no JavaScript changes required.


License
-------

- MIT https://github.com/aws/mit-0
