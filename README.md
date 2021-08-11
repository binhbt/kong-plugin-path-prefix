# kong-plugin-path-prefix
Build: luarocks make --pack-binary-rock  
# Support multiple prefix  
config.path_prefix = prefix1 prefix2 prefix2  

# Install for Kong  
`ENV KONG_PLUGINS bundled, path-prefix
RUN USER=root luarocks install https://github.com/binhbt/kong-plugin-path-prefix/raw/master/kong-plugin-path-prefix-0.1.0-1.all.rock
`  
A Kong plugin that rewrites the upstream request path. This can be useful if you have routes associated to a single service that all share the same path prefix.

For example, given `/foobar`, `/foobar/version`, and `/foobar/healthz` routes, the resulting upstream request routes will be `/`, `/version`, and `/healthz`, respectively, (assuming that `/foobar` is set as `config.path_prefix`).

This plugin is not compatible with APIs or any version older than Kong `0.14`.

## usage

Can be installed on either a service or individual routes.

### schema
| field          | explanation                                                          | default |
|----------------|----------------------------------------------------------------------|---------|
| `path_prefix`  | The prefix shared by all routes associated with the service.         | N/A     |
| `escape`       | Whether any hyphens in the path prefix should be escaped             | `true`  |

## development

Run `docker-compose up --build` to stand up an instance of Kong and Postgres. 
The `create.sh` script will scaffold a service that uses the plugin, along with several routes.
