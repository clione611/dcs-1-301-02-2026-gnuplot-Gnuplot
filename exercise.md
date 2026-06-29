# gnuplot 演習
## 1. 対話的に作成したグラフ

前半でGnuplotに対話的にコマンドを入力して作成したグラフ`force.png`がこの下に入る．
正しくできていれば，次の条件を満している．

- グラフの折れ線にはデータの点を示す印が入っている．
- 図の上に「力-たわみ」というタイトルが付いている．
- 軸には，縦軸「力(kN)」，横軸「たわみ(m)」のラベルが付いている．
- 図の右上に凡例が入っている．

![前半で作成したグラフがここに入る](force.png)

## 2. 関数のプロット

次の「みほん」の図と同じようになるように gnuplotの記述を追記せよ.

- 関数は $y = f1(x) =2x^2\sqrt{x}-5x^2$ と $\displaystyle y= f2(x) = \frac{x}{\log{x}}$ とする．
- xの範囲を $0 \leq x \leq 7$ に，yの範囲を $-20 \leq y \leq 15$にする．
- グラフのタイトル，x軸のラベル，y軸のラベルを付ける．
- 格子状の補助線を入れる．
- 凡例は，`f1(x)` と `f2(x)` にする．

![関数のプロット](funcplot.png)

```gnuplot {cmd=true output="html"}
set terminal svg

set xrange [0:7]
set yrange [-20:15]
set grid
set title "関数のプロット"
set xlabel "x"
set ylabel "y"

plot 2*x**2*sqrt(x)-5*x**2 title "f1(x)", \
     x/log(x) title "f2(x)"

```

## 3. 八王子の気温

次の図と同じようになるように gnuplotの記述を追記せよ.

- データは `weather2026.csv` から取り出す
  - CSV である (データが 「 , 」で区切られている)ことに注意
- データとして1列目をx軸，2から4列目をy軸に指定し，
折れ線グラフにし，凡例を付ける
- グラフのタイトル，x軸のラベル，y軸のラベルを付ける
- 格子状の補助線を入れる

![weather](weather2026.png)

```gnuplot {cmd=true, output="html"}
set terminal svg
set datafile separator ","

set xdata time
set timefmt "%Y/%m/%d"
set xtics format "%m/%d"

set grid
set title "八王子の気温"
set xlabel "日付"
set ylabel "気温(℃)"

plot "weather2026.csv" using 1:2 with lines title "最高気温", \
     "weather2026.csv" using 1:3 with lines title "最高気温(平年)", \
     "weather2026.csv" using 1:4 with lines title "最低気温", \
     "weather2026.csv" using 1:5 with lines title "最低気温(平年)"
```

## 4． 誕生月

次の「みほん」の図と同じようになるように gnuplotの記述を追記せよ.

![誕生日の月別人数のグラフ](birthMonth.png)

- データは `bm.txt` から取り出し，棒グラフにする
- y軸の範囲は $0 \le y \le 16$とする
- 棒グラフは水色(skyblue)で塗り潰し，棒の幅は 0.6 にする
- グラフのタイトルを付ける
- y軸のラベル「人」を付ける
- x軸の目盛には「1月」のように月が入る
- 格子状の補助線を入れる


```gnuplot {cmd=true, output="html"}
set terminal svg
unset key
set style fill solid
set boxwidth 0.6
set yrange [0:18]
set grid
set title "誕生日の月別人数"
set ylabel "人数"
set xlabel "誕生月"
plot "bm.txt" using 1:2:xtic(1) with boxes linecolor "skyblue"


```
