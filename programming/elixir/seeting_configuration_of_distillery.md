## Setting configuration of distillery

### VM Configuration

Distillery will automatically generate a vm.args file for you, which configures the VM with a name and secure cookie, however there are times where you may want to provide your own, but still take advantage of metadata provided by Distillery. In this case, you would put set vm_args: "path/to/file" in your environment or release configuration, and define a file like the following at the path you provided:

```
## Node name
-name <%= release_name %>@127.0.0.1

## Node cookie, used for distribution
-setcookie ${NODE_COOKIE}
```

This file will be templated using the EEx template engine, and you can use any of the overlay variables described here.

Also shown above is the use of dynamic configuration. If REPLACE_OS_VARS=true is set in the runtime environment, a copy of vm.args will be made with ${NODE_COOKIE} replaced with the value of the NODE_COOKIE environment variable.

### Application Configuration

Distillery will compile the configuration you define in config/config.exs (or whatever your config_path is set to) into a sys.config file, which is loaded by the VM at runtime to configure the applications in the release. A very important distinction to make here is that sys.config is not a dynamic file like config.exs, this means that if your config.exs file has a call to say System.get_env/1 in it, that call will be evaluated at compile-time, not run-time. If you need such configuration, either use the {:system, "ENV"} config options provided by your dependencies, and your application, or use dynamic configuration, as described above for vm.args. The dynamic configuration case has an additional limitation in Mix config files, because they can only be used within strings, making them unusable for configuration which requires integer values or other datastructures. In those situations, you have a couple of options:

Use vm.args with -<appname> <key> ${ENV_VAR} to configure those settings
Use Conform, or other configuration management libraries to help work around this limitation.

Reference: https://github.com/bitwalker/distillery/blob/55e24f4094e1c6570013380b157b5f759134ad1c/docs/Getting%20Started.md
