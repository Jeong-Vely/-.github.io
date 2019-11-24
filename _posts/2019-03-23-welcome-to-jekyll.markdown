---
layout: post
title:  "Yujin's Diary"
date:   2019-11-23 21:03:36 +0530
categories: Javascript NodeJS
---
I am Jeong Yu Jin majoring in media engineering at Kangwon National University. 

---나의 경험 ---
나의 경험으로는 전화번호부를 만들어 많은 사람들에게 편리함과 편의를 제공하였다. 

```javascript
const Razorpay = require('razorpay');

let rzp = Razorpay({
	key_id: 'KEY_ID',
	secret: 'name'
});

// capture request
rzp.capture(payment_id, cost)
	.then(function (data) {
		return 2;
	})
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
