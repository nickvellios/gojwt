# gojwt v0.0.1

gojwt is a barebones JSON Web Token implementation in Go.  I wrote this as a test for a future project.  As I get closer to that project I will begin to build this project out as needed.  Currently gojwt only supports the HMAC SHA Algorithm because that's all I needed.  Please feel free to contribute and add other algorithms.

Error handling needs some massaging.

More info on what a JSON Web Token is can be found here:  https://jwt.io/

### Usage

Create JWT:
```sh
claims := map[string]string{
  "user": "nick",
  "email": "nick@github.com",
}
expiration := 3600 // seconds
token := jwt.Generate(claims, expiration)
```

Decode JWT
```sh
payload := jwt.Decode(token)
fmt.Println("Hello " + payload["user"])
```

You can also decode directly from a cookie (neat?):

```sh
func SomeHttpHandler(w http.ResponseWriter, r *http.Request) {
	payload, err := jwt.DecodeFromCookie(r, "user")
	if err != nil {
		fmt.Fprint(w, "Something bad happened")
		return
	}
	fmt.Fprint(w, "Logged in.  Welcome back "+payload["user"])
}
```

License
----

Unlicense.  For more information, please refer to <http://unlicense.org/>
