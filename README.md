# Code-Based-Key-Exchange

参考文献

1.https://deneuville.github.io/files/PQC17.pdf

2.https://arxiv.org/pdf/1612.05572.pdf

3.https://eprint.iacr.org/2017/757.pdf

4.https://arxiv.org/pdf/1907.12754.pdf

# 20201114

次の目標は、符号を使った鍵交換です。

ouroborosというのが面白そうだと思ったけど、具体例がないし普通のMcElieceベースの鍵交換というのとも違う感じなのでわかりにくい。

私は私で単純に相互にエラーベクトルを送りあえばいいだけだと思っている。
例えば、アリスがボブと鍵交換したいと思えば、

「私はアリスです。ボブのエラーebを受け取りました」

「私はボブです。アリスのエラーeaを受け取りました」

とやっておき、H(ea^eb)=sk（Hはハッシュ関数、^はXOR、skは共有された秘密鍵）

とすれば、盗聴者は最終的にアリスとボブがどんな秘密鍵を共有したのかはわからないのではないかと思う。

ここで鍵交換を行うもの同士の自己紹介の部分をどう実現するかなのですが、受け取ったエラーベクトルのハッシュ値を、確認のために
送るか公開すれば同じ効果が得られると思う。（あまりスマートなやり方ではないが、素朴鍵交換といえばいいかなと思っている。）

ボブは自分の送ったエラーのハッシュ値とアリスが公開したハッシュ値が一致するかどうかで、正しい鍵交換ができたことを簡単に確かめることができる。

このような素朴な鍵交換でどこまでセキュリティが保護されるのかはわからないが、思いつく限りでは最も簡単だと思う。
このようなエラーのやり取りによってセッションキーを共有しても、Diffie-Hellmanと同じようにお互いの秘密鍵である
生成多項式はわからないのだからそんなに問題にはならないと思う。

公開鍵を使った認証方式には、私の過去の研究ノートにあるのでそのうち公開します。

ただこの鍵交換には認証機能がついていないので、現代風な認証機能付き鍵交換ではないというのが問題だと思う。
そこで、シンドロームベースのNiederreiter署名を使って認証の代わりにならないかと思っている。

符号ベースのFiat-Shamir署名は、私のリポジトリにあるCode Based Signatureに実装してあります。
