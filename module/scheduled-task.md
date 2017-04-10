# Scheduled Tasks

Scheduled tasks is sometimes a very important module in application. Keeling Js add support for easily setup schedule tasks if you put your scheduled tasks under the `schedule_directory` in your config file. 

Of course you can choose not to put anything inside this directory or just directly delete the directory. That is all fine, and Keeling Js will not load the scheduled tasks module.

But if you do want to have scheduled task, let's take a look of how these tasks are going to setup.

### Task File

All task files will be `.js` files and must be put under the directory of your `schedule_directory` . A sample task file will be like this:

```js
module.exports = {
    schedule: "* * * * * 1",
    task: function () {
        console.log("The answer of hello world");
    }
};
```

both `schedule` and `task` fields are necessary, while the schedule will be a cron-format scheduling string, and the task will be a function that does not take any parameter. 

Keeling Js use [Node Schedule](https://github.com/node-schedule/node-schedule). So you can check out cron format and other APIs shown there.



