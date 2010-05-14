
Codeigniter multi language support using google translate API.

Uses of this contribution:

1) No Need to maintain all text in different languages in our application.

Clarification: In the multilingual support sites -  we have text in English language. If we want to convert into different language we have to maintain other language text in our site.

If we use this contribution, no need of maintaining different languages text in our site.


2) It supports 'n' number of languages.

Clarification : If we use normal multilingual then we can use it for 2 or 3 languages. If we want another language then we want to write complete text in that language.

If we use this contribution, we can maintains 'n' number of languages.



Integration into CodeIgniter Site:


1) Create a new helper file tarnslate_helper.php in \system\helpers 

2) In application\config\autoload.php file add the below code:

	$autoload['helper'] = array('form', 'url','translate');

3) Process to integrating this contribution:


In the file header.php which is common for total site. 

Add the below code :

In head section add below meta tag to set the utf charset
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />

in Javascript code:

<script language="javascript" type="text/javascript">
 function lanfTrans(lan)
 {
   switch(lan)
   {
   case 'en': document.getElementById('dlang').value='en';document.langForm.submit(); break;
   case 'fr': document.getElementById('dlang').value='fr'; document.langForm.submit(); break;
   case 'es': document.getElementById('dlang').value='es'; document.langForm.submit(); break;
   } 
 }
</script>


in HTML code :

<form name="langForm" id="langForm" action="<?php echo base_url().'welcome/languages';?>" method="post"> 

<?php // 'welcome' - [Home page controller] ?>

<input type="hidden" name="dlang" id="dlang"> 

<?php // 'dlang' - [Language choosen] ?>

<input type="hidden" name="current" id="current" value="<?php echo substr(uri_string(),1,strlen(uri_string()));?>">

<?php // 'current' - [Current page url] ?>

<?php // [Language images] ?>
 
<img src="<?=base_url()?>images/fr.png" onClick="lanfTrans('fr');" width="16" height="11" title="To French"> &nbsp; 

<img src="<?=base_url()?>images/en.png" onClick="lanfTrans('en');" width="16" height="11" title="To English"> &nbsp;
<img src="<?=base_url()?>images/es_flag.gif" onClick="lanfTrans('es');" width="16" height="11" title="To Spanish"> &nbsp;

<?php echo form_close(); ?>


In the welcome / home page controller :

Add the below method

This method to assign language to session variable.

function languages()
	{
	   extract($_POST);
	   $this->session->set_userdata('language', $dlang);
	   $redirect_url = base_url().$current;
	   redirect($redirect_url);	
	
	}

Once create this mothod.if we want to use this functionality in the site then add the below code in the metods.

$data['lang'] = $this->session->userdata('language');

// assign those session variable to one variable.


In the view pages, use below code to translate one language to another.

<?php translate("Welcome to codeigniter",$lang);?>

It will convert these text according to language choosed.




Limitations:

1) This contribution is not working in offline mode.

2) At a time we can translate 5000 characters.


