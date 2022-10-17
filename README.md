### SimpleCalendar

Made with vanilla JavaScript.

**使い方**

HTMLに読み込ませます。
```javascript
<script type="text/javascript" src="simplecalendar.js" charset="utf-8"></script>
```

カレンダーを表示したい箇所に何らかのタグを置いてクラスかIDを付けます。
タグはdivでもいいです。なんでもいいです。
```javascript
<span class="simplecalendar"></span>
```

クラス、またはIDを指定してカレンダーを作成します。
document.querySelector で処理しますので、それ用の定義を書いてください。
```javascript
new SimpleCalendar('.simplecalendar')
```

### オプションパラメータ

カレンダーの設定を変更することができます。
第二引数にハッシュマップで定義します。
```javascript
new SimpleCalendar('.simplecalendar', {
  today: new Date('2022-10-01')
});
```

以下の定義を設定できます。

*today* [String][Date]

今日の日にちを設定できます。
対象の日にクラス名「today」が付与されます。

```javascript
new SimpleCalendar('.simplecalendar', {
  today: new Date('2022-10-01')
});
```

*holiday* [Array]

祝日を設定できます。
Array に YYYY-mm-dd 形式で祝日の日を定義します。

KSV で YYYY-mm-dd: 祝日名 でも定義できますが、祝日名は表示されず、Key の日付のみ処理します。

```javascript
new SimpleCalendar('.simplecalendar', {
  holiday: ['2022-01-01', '2022-01-02']
});
```

*datas* [Object]

KVS で定義します。
Key で指定した対象の日付に dataset.datas = value で設定されます。

```javascript
new SimpleCalendar('.simplecalendar', {
  datas: {
    '2022-10-10': 'hogehoge',
    '2022-10-11': 'fugafuga',
  }
});
```

*click* [Function(String YYYY-mm-dd, dataset, Element, Event)]

日付をクリックした時にコールされるメソッドです。
日付クリックで画面遷移したい場合に使えます。例えばブログ記事のリンク等に。

```javascript
new SimpleCalendar('.simplecalendar', {
  datas: {
    '2022-10-10': 'hogehoge',
    '2022-10-11': 'fugafuga',
  },
  click: function(day, dataset) {
    location.href = '/'+dataset.datas+'.html';
  }
});
```

*changeCalendar* [Function(new String, past String)]

カレンダーを変更した時に実行されます。
先月、来月、月変更、年変更の場合にコールされます。
holiday や datas の内容を読み込む時に利用できます。

```javascript
new SimpleCalendar('.simplecalendar', {
  datas: {
    '2022-10-10': 'hogehoge',
    '2022-10-11': 'fugafuga',
  },
  click: function(day, dataset) {
    location.href = '/'+dataset.datas+'.html';
  },
  changeCalendar: async function(new, past) {
    var data = await fetch('datas.json?date='+new Date(new).getFullYear());
		this.setDatas(await data.json());
  }
});
```

