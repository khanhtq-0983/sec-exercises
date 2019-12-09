Bài 1 : Chuyển số 1234 sang các hệ cơ số :
Hệ nhị phân : 10011010010
Hệ bát phân : 2322
Hệ thập lục phân :4d2
Hệ 36 : YA
Hệ 58 : a
Hệ 64 :TS

Bài 2:
function my_base64_encode($str)
{
    $base64 = str_split('ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/');
    $bit_pattern = '';
    $padding = 0;
    $encoded = '';
    foreach (str_split($str) as $char) {
        $bit_pattern .= sprintf('%08s', decbin(ord($char)));
    }
    $bit_pattern = str_split($bit_pattern, 6);
    $offset = count($bit_pattern) - 1;
    if (strlen($bit_pattern[$offset]) < 6) {
        $padding = 6 - strlen($bit_pattern[$offset]);
        $bit_pattern[$offset] .= str_repeat('0', $padding);
        $padding /= 2;
    }
    foreach ($bit_pattern as $bit6) {
        $index = bindec($bit6);
        $encoded .= $base64[$index];
    }
    return $encoded.str_repeat('=', $padding);
}
function my_base64_decode($str)
{
    $base64 = str_split('ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/');
    $bit_pattern = '';
    $padding = substr_count(substr(strrev($str), 0, 2), '=');
    $decoded = '';
    foreach (str_split($str) as $b64_encoded) {
        $bit_pattern .= sprintf('%06s', decbin(array_search($b64_encoded, $base64)));
    }
    $bit_pattern = str_split($bit_pattern, 8);
    if ($padding) {
        $bit_pattern = array_slice($bit_pattern, 0, -$padding);
    }
    foreach ($bit_pattern as $bin) {
        $decoded .= chr(bindec($bin));
    }
    return $decoded;
}

Bài 3 : sử dụng ceasar cipher decode 
FLAG_SwzgxBJSAMqwxxAU

Bài 4 :
