# Underpants
## A reverse HTTP proxy that authenticates requests through Google OAuth.

Suppose you are a Google Apps customer and suppose you want to restrict access to some web servers to just the folks in your organization. Like, for instance, if you're building your internal apps on AWS. Pain in the ass, right? So put underpants in between the world and your backends and you can use your Google credentials to get in.

## Installation

```
go get github.com/kellegous/underpants
```

## Configuration

Your underpants are configured through a silly little JSON file. Here's an example:
<pre>
{
  "host" : "underpants.company.com",
  "oauth" : {
    "domain"        : "company.com",
    "client-id"     : "oauth-client-id",
    "client-secret" : "oauth-client-secret"
  },
  "certs" : [
    {
      "crt" : "/path/to/crt.pem",
      "key" : "/path/to/key.pem"
    }
  ],
  "routes" : [
    {
      "from" : "public.company.com",
      "to"   : "localhost:8080"
    }
  ]
}
</pre>

The `certs` section is optional and its absense will cause your underpants proxy to operate on pure HTTP. The key file may be encrypted so
long as it is in encrypted PEM format with proper `Proc-Type` and `Dek-Info` headers. If you do not know what that means, just use openssl
and that is what you will end up with.

You can get your oauth-client-id and oauth-client-secret by creating a project on [Google's API Console](https://code.google.com/apis/console).

## Running

Just run it; it's an executable.

```
underpants
```

## Some TODO's
 * Handle non-transactional traffic, like web sockets.
