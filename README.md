# Пример использования

    <?php
    require_once 'LittleSMS.class.php';

    $user = 'my-login';            // логин указанный при регистрации или логин api-аккаунта http://littlesms.ru/my/accounts
    $key  = 'my-secret-api-key';   // API-key, узнать можно тут: http://littlesms.ru/my/api или тут: http://littlesms.ru/my/accounts, если используете логин api-аккаунта
    $ssl  = false;                 // использовать защищенное SSL-соединение

    $api = new LittleSMS($user, $key, $ssl);

    // запрос баланса
    echo 'Мой баланс: ' . $api->userBalance(), PHP_EOL;

    // отправка СМС
    $ids = $api->messageSend('79631112233', 'Бугагашенька!');
    if ($ids) {
      echo "ID отправленных СМС:\n";
      print_r($ids);
    } else {
      echo "Ошибки:\n";
      print_r($this->getResponse());
    }

    // запрос статуса сообщения
    $result = $api->messageStatus($ids);

    foreach ($result as $message_id => $status) {
        echo sprintf('Статус сообщения %s: %s', $message_id, $status), PHP_EOL;
    }

