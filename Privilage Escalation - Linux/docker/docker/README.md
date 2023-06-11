<!DOCTYPE html  PUBLIC '-//W3C//DTD XHTML 1.0 Transitional//EN'  'http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd'><html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta content="text/html; charset=utf-8" http-equiv="Content-Type"/>
<title>Docker</title>
</head><body>Escaliation by docker...<br/>
<br/>
<br/>
well fek!<br/>
<br/>
TLDR.<br/>
<br/>
<br/>
get onto machine..<br/>
<br/>
Identify that you are hosting docker<br/>
<br/>
IDentify that you are a member of the docker group<br/>
<br/>
Spawn a docker instance at root.<br/>
<br/>
Use an enumartion tool... Ie Linenum to speed this up.<br/>
<br/>
<img height="141" src="image.png" width="900"/><br/>
<br/>
<br/>
From here head on over to GTFO bins and see what can be done with the docker tools avaliable<br/>
<br/>
<img height="69" src="image 2.png" width="400"/><br/>
<br/>
<img height="229" src="image 3.png" width="600"/><br/>
<br/>
We meet these conditions<br/>
<br/>
docker run -v /:/mnt --rm -it &lt;image&gt; chroot /mnt sh <br/>
<img src="image 4.png"/><br/>
<br/>
<br/>
</body></html>