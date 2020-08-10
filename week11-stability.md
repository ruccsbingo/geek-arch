1. 导致系统不可用的原因有哪些？保障系统稳定高可用的方案有哪些？请分别列举并简述。
- CDN运营商故障
  - 对接多家CDN运营商，确保可以随时切换
- IDC机房故障
  - 多机房备份，确保可以随时切换
- 交换机故障
  - 多交换机备份，确保可以随时切换
- 机器故障
  - 多服务实列，LB做负载均衡
- 服务故障
  - 多服务实列，LB做负载均衡
- 数据库故障
  - 主从保证数据库非单点
- redis故障
  - redis集群模式，避免单点故障


请用你熟悉的编程语言写一个用户密码验证函数，
Boolean checkPW(String 用户ID，String 密码明文，String 密码密文)
返回密码是否正确boolean值，密码加密算法使用你认为合适的加密算法。
```go
func checkPW(userID string, clearText string , cipherText string ) bool {
	m := md5.New()
	d := m.Sum(userId+clearText)
	return string(d) == cipherText
}
```

引用
- https://blog.coderzh.com/2016/01/03/security-design/