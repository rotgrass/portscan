<?php
set_time_limit(0);
error_reporting(0);
$ports_input = '22,80,6379';
$hosts_input = '127.0.0.1';
$timeout = 0.5;
$ports = explode(',', $ports_input);
$hosts_array = explode('/', $hosts_input);
$ip = ip2long($hosts_array[0]);
$net_mask = intval($hosts_array[1]);
$range = pow(2, (32 - $net_mask));
$start = $ip >> (32 - $net_mask) << (32 - $net_mask);
for ($i = 0;$i < $range;$i++) {
    $h = long2ip($start + $i);
    foreach ($ports as $p) {
        $c = @fsockopen($h, intval($p), $en, $es, $timeout);
        if (is_resource($c)) {
            echo $h.':'.$p.' => open\n';
            fclose($c);
        } else {
            echo $h.':'.$p.' => '.$es.'\n';
        }
        ob_flush();
        flush();
    }
}
