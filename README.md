I always do the README last, so I apologize for the docs being crappy. This implementation however, is very straight forward.

This application is running atop Basho's rebar. Therefore, you can get a simple terminal-version running by following these directions:

1. Look in src/pusherl.app.src and replace the configurable pusher application variables with your application's credentials.
2. In your terminal (I'm assuming you have Erlang R14B02 or higher installed) do the following:

```bash
./rebar get-deps
./rebar compile
./rebar generate
```

and finally to start an interactive console:

```bash
./rel/pusherl/bin/pusherl console
```

3. You may now execute push commands to pusher with the following:

A quick caveat I'd like to point out. If you are building this as a stand-alone release (not in another otp app) to try it out, you will want to to the following:
On line 2 of rel/reltool.config you will see something like this

```erlang
 {lib_dirs, ["../../"]},
```

You will want to change it to this

```erlang
  {lib_dirs, ["../deps","../../"]},
```

Yes, include the comma at the end.

USAGE

```erlang
%% If you wish to perform synchronous pushes:
gen_server:call(pusherl_server, {push, {"ChannelName", "EventName", "Payload"}}).
	
%% If you wish to perform asynchronous pushes:
gen_server:cast(pusherl_server, {push, {"ChannelName", "EventName", "Payload"}}).
```

This application includes mochiweb for it's fantastic json de/encoding. I have not yet extensively tested that it works in all cases with json.

Thanks.
