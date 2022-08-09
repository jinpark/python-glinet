# pyglinet - json-rpc client for GL-Inet Router
This package aims to provide full access to the GL-Inet Luci API for firmware versions >= 4.0 via json-rpc. 

There is no official English documentation of the API yet. The lib parses the Chinese documentation from [here](https://dev.gl-inet.cn/docs/api_docs_page)  and dynamically 
creates the functions.

I initially created the client to automatically generate and write nordvpn wireguard configs to the router but then
found an elegant way to autogenerate calls for the whole api. 

The best way to navigate through the api is within an ipython shell. I may add in future a wrapper but for now you must
start the shell first and then load the module.

## Features
- Complete API support
- Dynamic method creation inclusive docstring from online documentation
- Api responses are represented recursively as objects, such that you can access all properties via '.'
- Cache for api description and hashed login
- Configure background thread to keep connection alive


## Installation:

```
#clone repository
git clone https://github.com/tomtana/python-glinet.git
cd python-glinet
```

Install package directly. The `-e` parameter lets you edit the files. 
If this is not needed to can also install without the `-e` parameter.
```
pip install -e .
```

Alternatively install it in an Python virtual environment (see [here](https://docs.python.org/3/tutorial/venv.html) 
for more infos)
```
python3 -m venv venv
source venv/bin/activate
pip install -e .
```
## Examples:

### Login
Login is as easy as that. If you modified your ip-address or other parameter, 
you need to pass them as parameter (see the documentation of the GlInet class for more details).

Per default the following steps are executed:
- if no password is passed
  - try to load from persistance (password stored as hash)
  - if no success ask via prompt
- try to load api reference from persistence, otherwise load it from the web
- persist settings
- start background thread to keep connectio alive

```python
glinet = GlInet()
glinet.login()
```

### API usage
First you need to generate an api object.
```python
client = glinet.get_api_client()
```
Now you can intuitively navigate the api using code completion and docstring. 



## ToDos:
- [x] Add dynamically docstring for API calls
- [x] Create pip compliant package
- [ ] Add tests
- [ ] Publish pip package
- [ ] Improve documentation
- [ ] Add wrapper for execution via terminal
