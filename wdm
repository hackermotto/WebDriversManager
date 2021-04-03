#!/bin/bash

echo "[+] WebDrivers Manager"
echo "--------------------------------"

cd ~/.local/bin/

WebDriversDir="webdrivers"
GeckoDriverDir="geckodriver"
ChromeDriverDir="chromedriver"

GeckoDriverPath="geckodriver"
ChromeDriverPath="chromedriver"

GeckoDriverVersion=`curl --silent https://api.github.com/repos/mozilla/geckodriver/tags | jq -r .[0].name`
ChromeDriverVersion=`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE`

function Initialize {
	echo "[+] Initializing .."

	if [ -d "$WebDriversDir" ]; then
		echo "[-] Directory $WebDriversDir/ exists."
	else
		echo "[-] Creating $WebDriversDir/ directory ..."
		mkdir $WebDriversDir
	fi	
}

function InstallGeckoDriver {
	echo "[+] Installing Gecko Webdriver .."
	
	if [ -d "$WebDriversDir/$GeckoDriverDir/" ]; then
		echo "[-] Directory $WebDriversDir/$GeckoDriverDir/ exists."
	else
		echo "[-] Creating $WebDriversDir/$GeckoDriverDir/ directory ..."
		mkdir $WebDriversDir/$GeckoDriverDir
	fi

	if [ -f "$WebDriversDir/$GeckoDriverDir/geckodriver-$GeckoDriverVersion" ]; then
		echo "[-] Version $GeckoDriverVersion already exists"
	else
		echo "[-] Downloading version $GeckoDriverVersion  .."
		wget https://github.com/mozilla/geckodriver/releases/download/$GeckoDriverVersion/geckodriver-$GeckoDriverVersion-linux64.tar.gz > /dev/null 2>&1
		tar -xvf geckodriver-$GeckoDriverVersion-linux64.tar.gz -C $WebDriversDir/$GeckoDriverDir/ > /dev/null 2>&1
		rm geckodriver-$GeckoDriverVersion-linux64.tar.gz

		mv $WebDriversDir/$GeckoDriverDir/geckodriver $WebDriversDir/$GeckoDriverDir/geckodriver-$GeckoDriverVersion
		chmod +x $WebDriversDir/$GeckoDriverDir/geckodriver-$GeckoDriverVersion
		ln -fs $WebDriversDir/$GeckoDriverDir/geckodriver-$GeckoDriverVersion ./$GeckoDriverPath
	fi
}

function UninstallGeckoDriver {
	echo "[+] Uninstalling Gecko Webdriver .."

	if [ -d "$WebDriversDir/$GeckoDriverDir/" ]; then
		echo "[-] Directory $WebDriversDir/$GeckoDriverDir/ exists."
		rm -rf $WebDriversDir/$GeckoDriverDir/
		rm $GeckoDriverPath
		echo "[-] Uninstalled Successfully."
	else
		echo "[-] No drivers was found !"
	fi	
}

function InstallChromeDriver {
	echo "[+] Installing Chrome Webdriver .."

	if [ -d "$WebDriversDir/$ChromeDriverDir/" ]; then
		echo "[-] Directory $WebDriversDir/$ChromeDriverDir/ exists."
	else
		echo "[-] Creating $WebDriversDir/$ChromeDriverDir/ directory ..."
		mkdir $WebDriversDir/$ChromeDriverDir/
	fi

	if [ -f "$WebDriversDir/$ChromeDriverDir/chromedriver-$ChromeDriverVersion" ];then
		echo "[-] Version $ChromeDriverVersion already exists."
	else
		echo "[-] Downloading version $ChromeDriverVersion  .."
		wget https://chromedriver.storage.googleapis.com/$ChromeDriverVersion/chromedriver_linux64.zip > /dev/null 2>&1
		unzip -o -d $WebDriversDir/$ChromeDriverDir/ chromedriver_linux64.zip > /dev/null 2>&1
		rm chromedriver_linux64.zip
		
		mv $WebDriversDir/$ChromeDriverDir/chromedriver $WebDriversDir/$ChromeDriverDir/chromedriver-$ChromeDriverVersion
		chmod +x $WebDriversDir/$ChromeDriverDir/chromedriver-$ChromeDriverVersion
		ln -fs $WebDriversDir/$ChromeDriverDir/chromedriver-$ChromeDriverVersion ./$ChromeDriverPath
	fi
}

function UninstallChromeDriver {
	echo "[+] Uninstalling Chrome Webdriver .."

	if [ -d "$WebDriversDir/$ChromeDriverDir/" ]; then
		echo "[-] Directory $WebDriversDir/$ChromeDriverDir/ exists."
		rm -rf $WebDriversDir/$ChromeDriverDir/
		rm $ChromeDriverPath
		echo "[-] Uninstalled Successfully."
	else
		echo "[-] No drivers was found !"
	fi	
}

Initialize

case $1 in 
	install)
		case $2 in
			gecko)
				InstallGeckoDriver
			;;
			chrome)
				InstallChromeDriver
			;;
		esac
	;;

	uninstall)
		case $2 in
			gecko)
				UninstallGeckoDriver
			;;
			chrome)
				UninstallChromeDriver
			;;
		esac
	;;

esac

echo "[-] Done."
