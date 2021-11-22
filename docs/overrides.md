# Přepisy PS modulů

##Packetery v2.1.9
- Soubor **packetery.php** na řádku **538**

  *Origin* 
  ```php
   $js = [
            'front.js?v=' . $this->version,
        ];
  ```
  *New* 
    ```php
   $this->context->controller->addJS($this->_path.'/views/js/front.js');
    ```
  aby jsme mohli override front.js
  

- Soubor **packetery.php** na řádku **765**
  přidána validace zda je odběr vážně na pobočce Zásilkovny 

  *Origin*
    ```php
  $orderData = Db::getInstance()->getRow(
            sprintf('SELECT `name_branch` FROM `%spacketery_order` WHERE `id_cart` = %d AND `is_ad` = 0', _DB_PREFIX_, (int)$params['order']->id_cart)
  );
  
  if (!$orderData) {
     return;
  }
    ```
  *New*
    ```php
    $orderData = Db::getInstance()->getRow(
            sprintf('SELECT `id_order`, `name_branch` FROM `%spacketery_order` WHERE `id_cart` = %d AND `is_ad` = 0', _DB_PREFIX_, (int)$params['order']->id_cart)
    );
  
    if (!$orderData || $orderData['id_order'] === NULL) {
            return;
    }
     ```
- Soubor **packetery.api.php** na řádku **225** změna aby prošla 100% sleva    
  *Origin*
    ```php
      $total = $order->total_paid;  
    ```
  *New*
    ```php
       $total = $order->total_products; //Fix for 100% sale 
  ```

- Soubor **front.js** změny viz commit pro uchování funcionality při one page checkoutu  https://bitbucket.org/integritty/tt_ps_starter/commits/12a6a7f9f3e525271d2406ba17b0ce1dbdfa61cd
  
