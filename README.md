# MdLt — LifeTech OCMS Core Framework Module

**MdLt** is the core application framework module of **LifeTech OCMS**. It provides foundational classes, functions, and services that enable modules, themes, and plugins to interact with the LifeTech OCMS system.

MdLt supports essential framework operations, including routing, HTTP request handling, API responses, database interactions, session management, authentication, and shared application utilities.

> **Important:** MdLt is framework infrastructure, not an example feature module. Developers building application features should use a functional module such as `MdBlog` as their practical example.

## Package information

The following metadata comes from the `v1.x` branch's `package.json`:

| Property | Value |
| --- | --- |
| Package name | `MdLt` |
| Package type | `module` |
| Current declared package version | `1.3.5` |
| Declared LifeTech OCMS version | `2.7.4` |
| Languages | PHP, HTML, CSS, JavaScript, LifeRazor |
| Declared dependencies | None (`[]`) |
| License | MIT |

**Version note:** The `ltVersion` value is the version recorded in package metadata; it should not be interpreted as a tested compatibility range without further release documentation.

## What MdLt provides

MdLt is intended to centralize framework-level functionality so feature modules do not need to reimplement common operations. Examples of shared responsibilities include:

- **Routing:** mapping incoming requests to application handlers.
- **Request handling:** accessing incoming HTTP request data.
- **API responses:** returning consistent response structures and status information.
- **Data access:** providing shared database and model functionality.
- **Sessions and authentication:** supporting user/session-aware application behavior.
- **Shared services:** making reusable framework logic available to modules and other packages.

The exact classes, methods, and signatures should be checked against the source files in the version of MdLt installed in your project.

## Repository structure

The `v1.x` branch currently contains these top-level items:

```text
MdLt/
├── Controllers/
├── Export/
├── Models/
├── Services/
├── Views/
├── ddm/
├── LtSiteInfo.service.lifetech
├── package.json
├── README.md
└── LICENSE
```

| Directory / file | Role |
| --- | --- |
| `Controllers/` | Framework request handlers and controller-related code |
| `Models/` | Model and data-related code |
| `Services/` | Shared application services |
| `Views/` | View resources supplied with the package |
| `ddm/` | DDM-related package resources |
| `Export/` | Exported package resources |
| `LtSiteInfo.service.lifetech` | Package-provided service file; inspect its source before relying on its interface |
| `package.json` | Package identity, version, language, and dependency metadata |

These descriptions indicate the folders' intended roles, not a complete inventory of their implementations.

## How MdLt fits into LifeTech OCMS

A typical LifeTech OCMS feature uses framework functionality in the following way:

```text
Client / browser
      |
      v
LifeTech OCMS routing and request handling
      |
      v
Feature module controller (for example, MdBlog)
      |
      v
Feature module service
      |
      v
Feature module model / data operations
      |
      v
Response returned to the client
```

MdLt supplies shared framework functionality used along this request lifecycle. A feature module implements its own application-specific rules, such as creating a blog category or retrieving blog posts.

### Conceptual example

The following illustrates the separation of responsibilities. **It is not a copy of a specific MdLt source file.**

```php
// A feature controller delegates application logic to its service.
// Framework request/response utilities are provided by LifeTech OCMS.

class BlogCategoryController
{
    public function index()
    {
        $service = new BlogCategoryService();
        $categories = $service->getCategories();

        // Return $categories using the response API available
        // in your installed LifeTech OCMS version.
    }
}
```

For working route declarations and real controller/service implementations, consult the module development documentation and the MdBlog module source.

## Using MdLt in a LifeTech OCMS project

MdLt is a framework-level package. Before installing, replacing, or updating it:

1. Confirm the version of LifeTech OCMS running in your environment.
2. Review `package.json` and the release history of the branch or tag you intend to use.
3. Back up your existing application and database.
4. Follow the **official module installation procedure** for your LifeTech OCMS release.
5. Verify routing, authentication, session handling, and the modules that depend on shared framework functionality.

Do not treat a manual copy of this repository as a documented installation method unless your LifeTech OCMS deployment procedure explicitly supports it.

## Development and extension

When developing against MdLt:

- Keep feature-specific business logic inside the relevant feature module.
- Reuse established framework classes and services instead of duplicating them.
- Check method signatures and namespaces in the checked-out version before calling them.
- Test changes to shared services against existing modules and themes.
- Use versioned releases/tags to track changes to framework behavior.

## Documentation and practical examples

- [LifeTech OCMS documentation](https://www.lifetech.host/hubs/Docs)
- [Module development documentation](https://github.com/lifetechOCMS/docs/tree/master/backend-development/module-dev)
- [LifeTech OCMS core repository](https://github.com/lifetechOCMS/lifetechocms)
- [MdLt repository](https://github.com/lifetechOCMS/MdLt)

## Reporting issues

For framework-related bugs, observations, and improvement requests, use the [LifeTech OCMS issue tracker](https://github.com/lifetechOCMS/lifetechocms/issues). Include the LifeTech OCMS version, MdLt version, steps to reproduce, expected behavior, and relevant error messages. Remove credentials and other secrets before sharing logs.

## License

MdLt is published with an [MIT license](LICENSE). See the license file for the complete terms.
