-module(bf_chat_main_controller, [Req]).
-compile(export_all).

% POST /push/sender/1/receptor/2/msg/hola
push('POST', []) ->
    redo:start_link(),
    redo:cmd(["RPUSH","queue.chat:"++Req:post_param("rcp")++":"++Req:post_param("ems"),Req:post_param("rsp")]),
    {output, "Ok"}.
 
pop('POST', []) ->
    redo:start_link(),
    Value = redo:cmd(["LPOP","queue.chat:"++Req:post_param("ems")++":"++Req:post_param("rcp")]),
    {output, Value}.
    
pushRedis('GET', []) ->
    redo:start_link(),
    redo:cmd(["SET","key","hola"]),
    {output, "Ok"}.
  