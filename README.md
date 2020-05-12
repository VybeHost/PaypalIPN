# Paypal-IPN

Une classe de notification instantanée de paiement (IPN) de PayPal pour Laravel.

Utilisez `PaypalIPNListener` dans votre script PHP IPN pour gérer l'encodage 
de données POST, renvoi à PayPal, et analyse de la réponse de PayPal.

Exemple d'utilisation :
```php
use Niroxy\PaypalIPN\PaypalIPNListener;

public function paypalIpn()
{
  $ipn = new PaypalIPNListener();
  $ipn->useSandbox(); // Si vous voulez utiliser le bac à sable de PayPal
  $verified = $ipn->verifyIPN();
  $all_receiver_email = [ 'test@gmail.com' ];

  $receiver_email_found = false;
  foreach ($all_receiver_email as $email) {
    if(strtolower($_POST['receiver_email']) == strtolower($email)) {
      $receiver_email_found = true;
      break;
    }
  }

  if($verified) {
    if($receiver_email_found) {
      // Vérifiez la variable POST et insérez votre code ici
    } else {
      die('Quelque chose a mal tourné dans le paiement');
    }
  } else {
    die('Quelque chose a mal tourné dans le paiement');
  }
}
```

Installation
--------

`composer require niroxy/vybe-paypal-ipn`
