@echo off
echo.
echo.
echo		Changing the RDP PORT by ekstrah
echo		Support OS : Windows 10, Windows 7
echo.
set /p port=input port number : 
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v PortNumber /t REG_DWORD /d %port% /f
if errorlevel 1 (
	cls
	echo.
	echo.
	echo right click and run as administration
	pause>nul
	exit
)
netsh advfirewall firewall add rule name="RDP %port%" dir=in action=allow protocol=tcp localport=%port%
net stop /y TermService
net start /y TermService
echo everything has been completed
pause>nul
exit