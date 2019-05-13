# Error:  cache lookup failed for type on Postgresql

`ERROR:  cache lookup failed for type xxxx` 에러는 type 을 지우고서 reconnection 을 하지 않아 기존의 type cache 에 문제가 생겨 발생한다.

따라서 postgres 에서 type 의 변경이 있었을 경우 **반드시** 모든 기존 connection 들을 끊어주어야 한다.
