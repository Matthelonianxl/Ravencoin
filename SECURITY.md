# Security Policy

## Supported Versions

Use this section to tell people about which versions of your project are
currently being supported with security updates.

| Version | Supported          |
| ------- | ------------------ |
| 5.1.x   | :white_check_mark: |
| 5.0.x   | :x:                |
| 4.0.x   | :white_check_mark: |
| < 4.0   | :x:                |

## Reporting a Vulnerability

Use this section to tell people how to report a vulnerability.

Tell them where to go, how often they can expect to get an update on a
reported vulnerability, what to expect if the vulnerability is accepted or
declined, etc.
<?php
/********************************************************************
Product		: Bitpay Gateway for Payage
Date		: 7 March 2018
Copyright	: Les Arbres Design 2010-2018
Contact		: http://www.lesarbresdesign.info
Licence		: GNU General Public License
*********************************************************************/
defined('_JEXEC') or die('Restricted Access');

class Payage_BitPay_LesArbresInstallerScript
{
public function preflight($type, $parent) 
{
	$app = JFactory::getApplication();
    $payage_xml_file = JPATH_ADMINISTRATOR.'/components/com_payage/payage.xml';
    if (!file_exists($payage_xml_file))
		{
        $app->enqueueMessage("Please install Payage before installing gateway addons", 'error');
		return false;
		}
        
	$xml_array = JInstaller::parseXMLInstallFile($payage_xml_file);
	$payage_version = $xml_array['version'];
	if (version_compare($payage_version,"2.07","<"))
		{
        $app->enqueueMessage("BitPay requires at least Payage 2.11. Please install the latest version of Payage first.", 'error');
		return false;
		}
    return true;
}

//-------------------------------------------------------------------------------
// Called at uninstall time
//
public function uninstall($parent)
{
    $app = JFactory::getApplication();
    $app->enqueueMessage("BitPay gateway for Payage has been uninstalled.");
}

//-------------------------------------------------------------------------------
// The main install function
//
public function postflight($type, $parent)
{
}

}
