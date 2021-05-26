---
title: "三角関数の話"
emoji: "🤖"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["数学","三角関数"]
published: false
---

## はじめに

度々、三角関数不要論が取りざたされます。そもそも、三角関数にあまり良いイメージを持っていない人はわりと多いのではないかと思います。サイン、コサイン、タンジェントの定義はわかっても、そこからごちゃごちゃ出てくる公式の数々に圧倒され、加法定理の公式を「咲いたコスモスコスモス咲いた」のように唱えて覚え、そこから倍角公式だの半角公式だのも出てきて、さらに$\sin(-x)=-\sin(x)$だけど$\cos(-x)=\cos(x)$みたいにサインは符号が入れ替わるけどコサインは入れ替わらないみたいなやつから、$\sin(\theta + \pi/2) = \cos(\theta)$みたいにサインとコサインが入れ替わる奴まで出てきて、イヤになった挙句に社会に出たらそんなの全然でてこなくて、うっかり「三角関数なんて不要だ」などと言おうものなら袋叩きに会う、そんな状況で三角関数と仲良くなるのは難しい気がします。

とりあえず「役に立つ」とか「知らなくても不都合は生じない」みたいな議論は他の人にお任せして、三角関数はもう少し面白いものだ、ということをつらつら書いてみたいと思います。想定読者は線形代数が終わったあたりの理工系の大学生です。

## 三角関数と数学の三分野

数学を大きく分けると「幾何学」「代数学」「解析学」の三つの分野にわけることができます。個人的に、三角関数の面白さは、これら三つの分野、「幾何学」「代数学」「解析学」の全てをつなぐ架け橋のような役目を果たすところにあると思っています。

「幾何学」は平面図形や空間図形など「広い意味での図形」を扱う学問です。中学で合同とか相似とかの概念を習ったと思いますが、大学ではさらに多様体論や位相幾何学といった抽象的な概念に発展していきます。「代数学」は、その名の通り「数」の代わりに文字を導入し、方程式などを解く学問です。連立方程式や二次方程式なんかを習ったと思います。連立方程式から行列などを学び、さらに「線形代数学」へと発展していきます。「解析学」は、極限を扱う学問で、要するに微分や積分などです。大学では複素関数論という美しい理論を学ぶことになります。

一見すると全く別の学問のように見える「幾何学」「代数学」「解析学」の三分野を、三角関数がどのように渡り歩くのかをみて行きましょう。

### 幾何学から解析学へ

いま教育現場で三角関数がどのように教えられているかは知りませんが、おそらく直角三角形を持ってきて、その斜辺と残りの二辺の比からサイン、コサイン、タンジェントを定義するところから入るんだと思います。

![def](trigonometric_function/def.png)

つまり、三角関数は幾何学の枠組みで導入されます。この後の公式達、例えば加法定理なんかも幾何学的に証明がなされるのではないかと思います。

さて、いまのカリキュラムだと、三角関数の微分は数学IIIで習うんですかね。こうして、まずは幾何学的に定義されたはずの三角関数が、解析学に足を踏み入れることになります。証明や定義はさておき、サインとコサインの微分だけ書いてみましょう。

$$
\begin{aligned}
\frac{d}{d\theta} \sin \theta &= \cos \theta, \\
\frac{d}{d\theta} \cos \theta &= -\sin \theta
\end{aligned}
$$

このように、サインとコサインは微分で互いに入れ替わり、コサインがサインになる時には負符号がつくのでした。

せっかくお互いに入れ替わる性質があるので、それを工夫して表現してみましょう。$\sin \theta$を$\vec{s}$、$\cos \theta$を$\vec{c}$とベクトルで書いてみます。そして、

$$
a \vec{c} + b \vec{s} = 
\begin{pmatrix}
a\\
b
\end{pmatrix}
$$

と表記することにしましょう。微分すると$\vec{c}$は$-\vec{s}$に、$\vec{s}$は$\vec{c}$になるのですから、微分を以下のように行列で表現することができます。

$$
\frac{d}{d\theta} \equiv A = 
\begin{pmatrix}
0 & -1\\
1 & 0 
\end{pmatrix}
$$

さて、この行列$A$をよく見てみましょう。行列の性質は、単位ベクトルにかけて見るとわかります。

$$
\begin{aligned}
A
\begin{pmatrix}
1\\
0 
\end{pmatrix}
&=
\begin{pmatrix}
0\\
1 
\end{pmatrix}\\
A
\begin{pmatrix}
0\\
1 
\end{pmatrix}
&=
\begin{pmatrix}
-1\\
0
\end{pmatrix}
\end{aligned}
$$

図示するとこんな感じです

![def](trigonometric_function/rotate_a.png)

この行列$A$は、反時計回りに90度回転させる演算だということがわかります。**すなわち、サインやコサインにとって微分とは90度回す処理に他なりません**。

そう思って公式をならべてみると、確かに微分と90度回す($\pi/2$を足す)処理が同じ結果となることがわかります。

$$
\begin{aligned}
\frac{d}{d\theta} \sin \theta &= \cos \theta, \\
\sin(\theta + \pi/2) &= \cos \theta\\
\frac{d}{d\theta} \cos \theta &= -\sin \theta \\
\cos(\theta + \pi/2) &= -\sin \theta
\end{aligned}
$$

微分という解析学の処理が、回転という幾何学の処理と繋がりました。

### 解析学から線形代数へ

先ほど、微分を行列で表しました。

$$
\frac{d}{d\theta} \equiv A = 
\begin{pmatrix}
0 & -1\\
1 & 0 
\end{pmatrix}
$$

さて、微分を二度演算すると二階微分になります。これを行列で表現すると、同じ行列を二度かけることに対応します。見てみましょう。

$$
\frac{d^2}{d\theta^2} = A^2 = 
\begin{pmatrix}
-1 & 0\\
0 & -1 
\end{pmatrix} = -I
$$


ただし、$I$は単位行列です。これは、サインやコサインを二回微分すると、単に自分に負符号がつくだけであることを表しています。行列とベクトルの言葉で書くとこんな感じです。

$$
\begin{aligned}
A^2 \vec{s} &= - \vec{s} \\
A^2 \vec{c} &= - \vec{c}
\end{aligned}
$$

さて、行列をあるベクトルにかけた時、自分自身の定数倍になる場合、そのベクトルをその行列の固有ベクトル、でてきた定数を固有値と呼ぶのでした。この固有ベクトルという概念は関数にも適用されます。つまり、**サインやコサインは二階微分演算子の固有関数です**。

サインやコサインが一階微分でお互いに入れ替わり、二階微分演算子では固有関数になるという事実は非常に大事です。これは、サインやコサインが微分という演算子に対して基底を張ることを意味するからです。サインやコサインから見ると微分は行列のように見え、微分から見るとサインやコサインはベクトルのように見えます。こうして、三角関数が線形代数と繋がります。

サインやコサインが基底となる、ということを利用した解析がフーリエ級数展開やフーリエ変換となります。大学の数学では線形偏微分方程式をフーリエ変換で解くというのをやると思いますが、そういうことができるのは、サイン、コサインが微分演算子の固有関数となるからです。

### 複素平面へ

サインやコサインにとって微分演算子は行列のように見え、この行列は二回かけると$-I$になるのでした。$I$は単位行列で、行列の世界の1のようなものです。さて、この「二回かけると-1になる量」として、虚数単位$i$を思い出しますね。なので、この行列をかける操作と虚数単位$i$をかける操作を結びつけることができそうです。

虚数単位$i$は、二乗すると$-1$になる、つまり$i^2=-1$となる他は普通の変数のように扱えます。ここから$i$をかけるという操作を、行列$A$をかける操作と同じようにするためには、

$$
z = \cos \theta + i \sin \theta
$$

という量を考えれば良いことがわかります。$z$に$i$をかけてみましょう。

$$
\begin{aligned}
iz &= i\cos \theta + i^2 \sin \theta \\
&= i\cos \theta - \sin \theta \\
&= -\sin \theta + i \cos\theta
\end{aligned}
$$

$z$と$iz$の実部と虚部を見ると、$\cos \theta$が$-\sin \theta$に、$\sin \theta$が$\cos \theta$になっており、確かに微分されていることがわかります。図示はしませんが、これが複素平面において反時計回りに90度の回転を表してることは、理工系の大学生なら知っていることでしょう。

さて、$i$をかける、という操作は、行列$A$をかけるという操作を実現するものでしたから、

$$
Az = iz
$$

です。さらに、行列$A$をかけるという操作は、もともと微分するという操作でした。

$$
\frac{d}{d\theta} z = i z
$$

ここから、$z$は

$$
z = \mathrm{e}^{i \theta}
$$

という関数であることがわかります(積分定数は1に選びました)。$z = \cos \theta + i \sin \theta$でしたから、結局、

$$
\mathrm{e}^{i \theta} = \cos \theta + i \sin \theta
$$

という式が導かれました。これはオイラーの公式と呼ばれるものです。特に、$\theta$として$\pi$を代入すると

$$
\mathrm{e}^{i \pi} = -1
$$

となります。こちらはオイラーの等式と呼ばれ、数学においてもっとも美しい式の一つと言われています。

さて、先ほどの式、

$$
\frac{d}{d\theta} z = i z
$$

を見てみましょう。これは、$z$が微分演算子に対して固有関数になっていることを表しています。

もともと、サインとコサインは微分すると入れ替わり、もう一度微分すると負符号がついてもとに戻るのでした。したがって、うまく線形結合を作ると、一階微分で(定数倍を除き)自分自身に戻るような関数を作ることができます。それが$\cos \theta + i \sin \theta$です。

サインやコサインは二階微分の固有関数でしたが、指数関数は一階微分の固有関数ですので、こっちで考えた方が楽そうだな、ということが想像できるでしょう。

こうして、サインやコサインを使ったフーリエ級数展開から、指数関数だけを使った複素フーリエ級数展開へと繋がっていくことになります。

## まとめ

「幾何学」で導入された三角関数の、微分という「解析学」における性質が、回転という「幾何学」的な性質を持つこと、また、それは行列という「代数学」の分野の言葉で表現できて、固有値や固有ベクトルといった概念が現れること、さらに複素数を導入することで、もともと二階微分演算子の固有関数だったサインやコサインをうまいことすると、一階微分の固有関数を作ることができて、それがオイラーの公式へとつながることを見てみました。

三角関数には、ここで紹介しきれなかった様々な面白い性質があり、もっといろんな分野に顔を出します。そもそも、数学とは本来、とても面白いものです。それが、大量にごちゃごちゃ現れる公式の海に溺れそうになりながらお経のように唱えて暗記して試験をやり過ごし、あまり意味を理解しないまま卒業して、イヤな思い出だけが残る、というのはとても悲しいことです。

この小文が、誰かの「へぇ、そうだったのか」につながることを願っています。

## 参考文献

* [三角関数は何に使えるのか 〜 サイン・コサイン・タンジェントの活躍 〜](https://qiita.com/drken/items/41b4ec6bde794cbcd0f6)
* [線形代数を学ぶ理由](https://qiita.com/kaityo256/items/872a2b2fdf977c0e3fbb)