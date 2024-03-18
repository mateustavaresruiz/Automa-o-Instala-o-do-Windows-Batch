@echo off

echo ===========================================================================
echo CHECKLIST DOS COMPUTADORES
echo ===========================================================================


for /f "tokens=*" %%A in ('hostname') do set "computerName=%%A"

set "prefix=CPU"

if "%computerName:~0,3%"=="%prefix%" (
    echo NOME DO COMPUTADOR CORRETO: %computerName%
echo =========================================================================== 
) else (
    echo NOME DO COMPUTADOR NAO ESTA CORRETO : %computerName%O 
    echo Altere o nome do computador antes de iniciar!
    sysdm.cpl  
    pause
    exit      
)

set "ips_desejados=192.168.0.70 192.168.0.71 192.168.0.72"

for /f "tokens=2 delims=:" %%a in ('ipconfig ^| findstr /i "IPv4 Address"') do (
    set ip_atual=%%a
)

set ip_atual=%ip_atual: =%
echo %ips_desejados% | find "%ip_atual%" >nul
if %errorlevel% equ 0 (
    echo IP FIXO CORRETO: %ip_atual%
) else (
    echo IP FIXO INCORRETO: %ip_atual%
    control ncpa.cpl
    pause
    exit
)

echo =========================================================================== 

set /p sevicos=Aplicar configuracoes (UAC / Firewall / Hosts / Plano de Energia) (s/n): 

if /i "%sevicos%"=="s" (

echo Adicionando o arquivo HOST:
echo (IP DESEJADO) >> %WINDIR%\System32\Drivers\Etc\Hosts
echo (IP DESEJADO) >> %WINDIR%\System32\Drivers\Etc\Hosts 
echo (IP DESEJADO) >> %WINDIR%\System32\Drivers\Etc\Hosts
echo (IP DESEJADO) >> %WINDIR%\System32\Drivers\Etc\Hosts
echo (IP DESEJADO) >> %WINDIR%\System32\Drivers\Etc\Hosts

echo Ajustando as opcoes de energia para nunca:
powercfg /x -monitor-timeout-ac 0
powercfg /x -standby-timeout-ac 0
powercfg /change standby-timeout-ac 0
powercfg /change standby-timeout-dc 0
powercfg /change hibernate-timeout-ac 0
powercfg /change hibernate-timeout-dc 0

echo Desativando o UAC:
powershell -Command "Set-ItemProperty -Path REGISTRY::HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System -Name ConsentPromptBehaviorAdmin -Value 0"

echo Desativando o firewall:
netsh advfirewall set allprofiles state off

) else (
    echo Instalacao recusada
)

echo ===========================================================================

set /p version=Qual versao do Office instalar (2010/2013/2016/2019/2021/0 - Nenhum): 

if "%version%"=="2010" (
    mkdir "C:\Users\%username%\Desktop\OFFICE2010"
    robocopy "\\COMPUTADOR\e\arquivos_checklist\office\OFFICE2010" "C:\Users\%username%\Desktop\OFFICE2010" /E /NFL /NDL /NJH /NJS
    set "instalar=C:\Users\%username%\Desktop\OFFICE2010\Office_HB_2010_Brazilian_x32.exe"
    rmdir /s /q  C:\Users\%username%\Desktop\OFFICE2010
) else (
    if "%version%"=="2013" (
        mkdir "C:\Users\%username%\Desktop\OFFICE2013"
        robocopy "\\COMPUTADOR\e\arquivos_checklist\office\OFFICE2013" "C:\Users\%username%\Desktop\OFFICE2013" /E /NFL /NDL /NJH /NJS
        set "instalar=C:\Users\%username%\Desktop\OFFICE2013\office\Setup32.exe"
        rmdir /s /q  C:\Users\%username%\Desktop\OFFICE2013
    ) else (
        if "%version%"=="2016" (
            mkdir "C:\Users\%username%\Desktop\OFFICE2016"
            robocopy "\\COMPUTADOR\e\arquivos_checklist\office\OFFICE2016" "C:\Users\%username%\Desktop\OFFICE2016" /E /NFL /NDL /NJH /NJS
            set "instalar=C:\Users\%username%\Desktop\OFFICE2016\office\Setup32.exe"
            rmdir /s /q  C:\Users\%username%\Desktop\OFFICE2016
        ) else (
            if "%version%"=="2019" (
                mkdir "C:\Users\%username%\Desktop\OFFICE2019"
                robocopy "\\COMPUTADOR\e\arquivos_checklist\office\OFFICE2019" "C:\Users\%username%\Desktop\OFFICE2019" /E /NFL /NDL /NJH /NJS
                set "instalar=C:\Users\%username%\Desktop\OFFICE2019\office\Setup32.exe"
                rmdir /s /q  C:\Users\%username%\Desktop\OFFICE2019
            ) else (
                if "%version%"=="2021" (
                    mkdir "C:\Users\%username%\Desktop\OFFICE2021"
                    robocopy "\\COMPUTADOR\e\arquivos_checklist\office\OFFICE2021" "C:\Users\%username%\Desktop\OFFICE2021" /E /NFL /NDL /NJH /NJS
                    set "instalar=C:\Users\%username%\Desktop\OFFICE2021\office\Setup32.exe"
                    rmdir /s /q  C:\Users\%username%\Desktop\OFFICE2021
                ) else (
                    if "%version%"=="0" (
                        echo Nenhum Office sera instalado.
                    ) else (
                        echo Opção inválida. Escolha entre 2010, 2013, 2016, 2019, 2021 ou 0.
                    )
                )
            )
        )
    )
)

if "%version%" neq "0" (
    echo Instalando a versao %version% do Office...
    start /wait "" "%instalar%"
)

echo ===========================================================================

set /p instalarProgramas=Deseja instalar os Programas padroes (s/n): 

if "%instalarProgramas%" == "s" (

echo Instalando o Adobe Acrobat Reader:
start /wait \\COMPUTADOR\e\arquivos_checklist\programas\Acrobat.exe /sAll /rs /msi EULA_ACCEPT=YES

echo Instalando o Google Chrome:
start /wait \\COMPUTADOR\e\arquivos_checklist\programas\Chrome.exe /silent /install

echo Instalando o Firefox:
msiexec /i \\COMPUTADOR\e\arquivos_checklist\programas\Firefox.msi /passive 

echo Instalando o Java:
start /wait \\COMPUTADOR\e\arquivos_checklist\programas\Java.exe /s

echo Instalando o Sophos Connect:
msiexec /i \\COMPUTADOR\e\arquivos_checklist\programas\SophosConnect.msi /passive 
mkdir C:\temp    
copy \\COMPUTADOR\e\arquivos_checklist\programas\COMPUTADORLIVA.scx C:\temp

echo Instalando o TeamViewer:
start /wait \\COMPUTADOR\e\arquivos_checklist\programas\Teamviewer.exe /S

echo Instalando o 7zip:
start /wait \\COMPUTADOR\e\arquivos_checklist\programas\7zip.exe /S

echo Instalando o PDFCreator:
start /wait \\COMPUTADOR\e\arquivos_checklist\programas\PDFCreator.exe /COMPONENTS="none" /NoIcons /DisableStartMenu /silent

echo Instalando o BDE:
start /wait \\COMPUTADOR\e\arquivos_checklist\programas\BDE64.exe 

echo Instalando o NETFRAMEWORK 3.5:
start /wait \\COMPUTADOR\e\arquivos_checklist\programas\dotnetfx35.exe

echo Instalando o Kaspersky:
start /wait \\COMPUTADOR\e\arquivos_checklist\programas\Kaspersky.exe /s

) else (
echo Nenhum programa sera instalado
echo ===========================================================================
pause
exit
)
pause


