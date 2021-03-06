# HttpAbstraction

Reusable server side HTTP client for standard and OAuth2 web or API transactions. This is something I wrote because OAuth2 is pretty much the standard and I've not had to authenticate against anything else for a while now. 

## Installation

Use NuGet to install https://www.nuget.org/packages/HttpAbstraction.Client

	Install-Package HttpAbstraction.Client

## Example

```cs
var grantOptions = new ResourceOwnerGrantOptions()
{
	UserName = [username],
	Password = [password],
};

var options = new OAuth2ClientOptions<ResourceOwnerGrantOptions>(grantOptions)
{
	BaseUri = "https://api.example.com/",
	TokenPath = "oauth2/v1/token/",
	ClientId = [yourapiclientid],
	ClientSecret = [yourapisecret],
	HasIntrospection = true, //Only if expiration/claims are returned in separate call to oauth2/v1/token/introspection
};

var client = new OAuth2Client<ResourceOwnerGrantOptions>(options);
var users = client.Get<List<User>>("users"); //Just an example

//You want to re-use HttpClient so do not put in using statement as this can cause network socket exhaustion
//Be sure to dispose client

```
