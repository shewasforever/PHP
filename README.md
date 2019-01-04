# 抓取页面（php）
<?php
function getAccessToken($url,$appkey,$appSecret){
	$curl = curl_init();
	//设置抓取的url
	curl_setopt($curl, CURLOPT_URL, $url);
	//设置头文件的信息作为数据流输出
	curl_setopt($curl, CURLOPT_HEADER, 0);
	//设置获取的信息以文件流的形式返回，而不是直接输出。
	curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
	//设置post方式提交
	curl_setopt($curl, CURLOPT_POST, true);
	//设置post数据
	$data = json_encode(array("appKey" =>$appkey,"appSecret" =>$appSecret));
	$date = addcslashes($data,'"');
	$post_data = array("data" => $date);
	curl_setopt($curl, CURLOPT_POSTFIELDS, $post_data);
	//执行命令
	$response = curl_exec($curl);
	//关闭URL请求
	curl_close($curl);
	//显示获得的数据
	return $response;
}
header("Content-type:text/html;charset=utf-8");//防止中文乱码
$appkey = "hndhkm2017";
$appSecret = "23e0635d472e822e6d6a50cade0f4e1a";
$url = "http://www.hndhkm.com/ecservice/index.php/";
$a = getAccessToken($url,$appkey,$appSecret);
$response = json_decode(getAccessToken($url,$appkey,$appSecret),true);
print_r($response) ;
 echo $a;
