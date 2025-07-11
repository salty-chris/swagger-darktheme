# swagger-darktheme
This project is to help save eyeballs. Swaggerdocs shouldn't just be for people who work during the day in brightly lit offices.
As of initial upload: It is a work-in-progress, but many elements are themed (and the file is a mess)

<img width="360" height="244" alt="image" src="https://github.com/user-attachments/assets/ca968ac1-df17-437b-9662-b6af2c281d89" />

---
# Versioning stuff
The version this is tested with is OpenAPI 3.1
---

# Rough instructions

If you are running fastapi, you will need to create a directory like "static" in the root directory of your project.
Then copy swagger-dark.css there.

Then in your main.py (or wherever you run your fastapi from) set-up this block:

The important parts here are disabling docs_url, you could techniclaly leave the rest as whatever or unset.

app = FastAPI(docs_url=None,
              redoc_url=None,
              title="Your API Docs Title",
              description="Some description",
              swagger_ui_parameters={
                  "defaultModelsExpandDepth": -1,
                  "defaultModelExpandDepth": 0,
              }
              )


And th en this block:
This one is basically replacing the docs page served by FastAPI with a new "dark" themed one.
@app.get("/docs", include_in_schema=False)
async def custom_swagger_ui_html():
    return get_swagger_ui_html(
        openapi_url=app.openapi_url,
        title="API Docs - Salty Dark Theme",
        swagger_css_url="/static/swagger-dark.css",
    )
