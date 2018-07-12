.NET Core Angular App with OpenId Connect Authentication
--------------------------------------------------------

This repository contains a modified version of the .NET Core Angular template application, which has been enhanced with OpenId Connect implicit flow authentication. It is intended to be used for Azure Active Directory authentication. The original template was gneerated with

```
dotnet new angular
```

And you can [browse the changes](https://github.com/hansenms/dotnet-angular-oidc/compare/original-template...master) that were made to the template. 

The example uses the Damien Bowden's OpenID Connect Certified [angular-auth-oidc-client](https://github.com/damienbod/angular-auth-oidc-client) module and the implementation is *heavily inspired* the example angular application in [https://github.com/damienbod/dotnet-template-angular](https://github.com/damienbod/dotnet-template-angular) with some changes. Specifically:

1. The [https://github.com/damienbod/dotnet-template-angular](https://github.com/damienbod/dotnet-template-angular) example uses static (downloaded versions of the openid-configuration and keys). This was needed because the Azure Active Directory endpoints do not allow Cross Origin Resourece Sharing (CORS). In this example, a `ConfigController` has been implemented to allow the backend application to do the discovery. That way changes to those backend configurations (such as keys) will be automatically loaded. 
2. This example allows both [v1.0 and v2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-compare) of the Azure Active Directory Endpoints.

To use the example, define the following application settings:

```json
{
  "oidc": {
    "issuer": "Oauth2-Issuer-Url",
    "client_id":"CLIENT-APP-ID",
    "scope": "openid profile email https://graph.microsoft.com/User.Read",
    "resource": ""
  }
}
```

If you use a v1.0 AAD endpoint, you will need to create your application registration in the Azure Portal (e.g., [https://portal.azure.com](https://portal.azure.com)) in the [Active Directory Application registration section](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Subsequently, the configuration would look something like:

```json
{
  "oidc": {
    "issuer": "https://login.microsoftonline.com/TENANT-ID/",
    "client_id":"CLIENT-APP-ID",
    "scope": "openid",
    "resource": "https://graph.microsoft.com/"
  }
}
```

For a v2.0 AAD endpoint configuration, you will need to use the new Microsoft App Registration Portal ([https://apps.dev.microsoft.com/](https://apps.dev.microsoft.com/)). The configuration would look like:

```json
{
  "oidc": {
    "issuer": "https://login.microsoftonline.com/TENANT-ID/v2.0/",
    "client_id":"CLIENT-APP-ID",
    "scope": "openid profile email https://graph.microsoft.com/User.Read",
    "resource": ""
  }
}
```

The application settings can be defined in the [`appsettings.json`](appsettings.json) file, using environment variables (app settings in a Web App), or using the `user-secrets` feature of the `dotnet` CLI:

```
dotnet user-secrets set oidc:issuer "https://login.microsoftonline.com/TENANT/v2.0/"
dotnet user-secrets set oidc:client_id "CLIENT-ID"
dotnet user-secrets set oidc:scope "openid profile email https://graph.microsoft.com/User.Read"
```

