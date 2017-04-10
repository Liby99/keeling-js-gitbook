# Configuration

You definitely want to configure your server. Keeling Js requires the user to specifically put a config JSON file under `data` directory \(although the `data` directory and `config.json` file should both be created if you installed Keeling Js from scratch\). But lets' take a look into this.

\(for those who doesn't has a `config.json` file in `data` directory:\)

```
$ mkdir data
$ vim config.json
```

Copy all these into the file and save:

```js
{
    "debug": true,
    "name": "Keeling Js Default",
    "port": 21023,
    "session_secret": "keeling-session",
    "default_page": "index",
    "error_page": "error",
    "public_directory": "public",
    "ajax_directory": "ajax",
    "router_directory": "router",
    "schedule_directory": "schedule"
}
```

Note that you can delete any entry if you think you are going to only use the default value \(just shown above\).

Lets take a close look of what these parameters are.

| Entry | Type | Default | Usage |
| :--- | :--- | :--- | :--- |
| `debug` | `<boolean>` | `true` | Show debug info or not. While Keeling Js itself is using the debug module, you can also fetch the debug module and use it for debugging. |
| `name` | `<string>` | `"Keeling Js Default"` | Just a name for identification. No actual usage. |
| `port` | `<number>` | `21023` | Specifies which port is the server going to listen to. |
| `session_secret` | `<string>` | `"keeling-session"` | The secret key used by encoding the session cookie. For safety of your server side cookie info please change this. |
| `default_page` | `<string>` | `"index"` | This will be the default page being redirected when the user's request only contains "/". Here \`index\` will refer to the \`index.html\` in the actual file system. |
| `error_page` | `<string>` | `"error"` | This will be the default error page being redirected when encountering server error. You can also use it yourself. For more information please go to |
| `public_directory` | `<string>` | `"public"` | This specifies the directory that you store all the static and .html files that can be accessed by the user. If you changed this value, please be sure to rename the original public directory to the new one. For more detail please go to [Html & Static File](/methods.md). |
| `ajax_directory` | `<string>` | `"ajax"` | This specifies the directory that you store all the Ajax request handlers. For more detail please go to [Ajax Request](/ajax-request.md). If you changed this value, please be sure to rename the original ajax directory to the new one. |
| `router_directory` | `<string>` | `"router"` | This is the directory that you store all the router file corresponding to the .html files in the public directory. For more details please go to [Html & Static File](/methods.md). If you changed this value, please be sure to rename the original router directory to the new one |
| `schedule_directory` | `<string>` | `"schedule"` | This specifies the directory that you store all the scheduled events in. Please go to [scheduled events section](/scheduled-events.md) for more details. If you changed this value, please be sure to rename the original schedule directory to the new one |

 

