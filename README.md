.NET Core Angular App with OpenId Connect Authentication
--------------------------------------------------------

This repository contains a modified version of the .NET Core Angular template application, which has been enhanced with OpenId Connect implicit flow authentication. It is intended to be used for Azure Active Directory authentication. The original template was gneerated with

```
dotnet new angular
```

And you can browse the changes in this PR. 

The example uses the Damien Bowden's OpenID Connect Certified [angular-auth-oidc-client](https://github.com/damienbod/angular-auth-oidc-client) module and the implementation is heavily inspired the example angular application in [https://github.com/damienbod/dotnet-template-angular](https://github.com/damienbod/dotnet-template-angular) with some changes. Specifically:

1. The [https://github.com/damienbod/dotnet-template-angular](https://github.com/damienbod/dotnet-template-angular) example uses static (downloaded versions of the openid-configuration and keys). This was needed because the Azure Active Directory endpoints do not allow Cross Origin Resourece Sharing (CORS). In this example, a `ConfigController` has been implemented to allow the backend application to do the discovery. That way changes to to those backend configurations (such as keys) will be automatically loaded. 
2. This example allows both [v1.0 and v2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-compare) of the Azure Active Directory Endpoints.