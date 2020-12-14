<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

| 7    | 6    | 5    | 4(2²) | 3    | 2(2¹) | 1(2⁰) | 位数 |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| S₄(1) | S₃(0) | S₂(1) |  | S₁(1) |  |  | 信息位 |
|      |      |      | r₂ |      | r₁ | r₀ | 校验位 |

$$
2^r >= m+r+1
$$

> m代表传输数据的位数，r代表校验位的位数。发送数据4位时，r最小是3；发送数据5位时，r最小是4。上表中传输数据以1011举例。  