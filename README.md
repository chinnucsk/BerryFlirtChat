BerryFlirtChat
==============

Erlang + ChicagoBoss + Redis

_Step 1._ Install Erlang.

_Step 2._ Download Chicago Boss and extract the archive.

_Step 3._ Get thee to a terminal

    cd ChicagoBoss
    ./rebar get-deps # only needed if you downloaded from GitHub
    ./rebar compile
    make
    make app PROJECT=rahm
    cd ../rahm

_Step 4._ Write an application. Put this into `src/controller/rahm_greeting_controller.erl`:

```erlang
-module(rahm_greeting_controller, [Req]).
-compile(export_all).
 
hello('GET', []) ->
    {output, "<strong>Rahm says hello!</strong>"}.
```

_Step 5._ Start the development server

    ./init-dev.sh

_Step 6._ Try it out in a web browser: `http://localhost:8001/greeting/hello`

_Step 7._ Stop the development server

    q().

_Step 8._ Write a conformance test. Put this into `src/test/functional/rahm_test.erl`:
(you will need a copy of boss.config named boss._test_.config and reference a database for testing in this config file if you like)

```erlang
-module(rahm_test).
-compile(export_all).
 
start() ->
    boss_web_test:get_request("/greeting/hello", [],
        [ fun boss_assert:http_ok/1,
            fun(Res) -> boss_assert:tag_with_text("strong", 
                "Rahm says hello!", Res) end ], []).
```

_Step 9._ Build for production and run the conformance test

    ./rebar compile
    ./rebar boss c=test_functional

Step 10. There is no step 10!

Just kidding, you need to start the production server.

    ./init.sh start

And if you need to stop it:

    ./init.sh stop

Now ask all your friends to visit your web page and try to get Rahm to stop saying hello.

It simply can't be done!

Furthermore, you can hot code reload by performing two and a half simple extra steps:

    0.5) Upload new the code
    1) ./rebar compile
    2) ./init.sh reload

