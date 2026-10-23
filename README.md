# Torihito(鳥人)サーバーミドルウェア

## 概要
comlab(BBSバックエンド)をホストするために生まれたサーバーミドルウェア。
ホビーから生まれた本格アプリ。新しいサービスを後から差し込める構成を目指す。

## 目的
- DB(SQLite)を中間層経由で扱い、別DBへ差し替え可能にする
- Node.js から Bun へ移行しても動くよう、Express 非依存の階層を挟む
- TypeScript の学習も兼ねる(まずインターフェースから .ts 化)

## 構成(Router > MainRouter > Express/Bun)
- Router.js: 最上位。servicesを集めてMainRouterに登録し、注入されたadapterで変換
- MainRouter.js: フレームワーク非依存のルート表と照合(改名予定、候補: RouteTable)
- adapters/: toExpress / toBun(Web標準の Request/Response と相互変換)
- サービスは routes ゲッターで [method, path, handler] の配列を返す
- 依存(adapter, ctx)は引数で注入する

## 決定事項
- handlerはWeb標準の Request/Response 形式
- OpenAPI(YAML)による定義・検証は後回し
- Service/Repository/Storage の細かい分割は維持(個別テストのため)

## 未決・次の作業
- 既存BBSのhandlerを (req, res) から (request, ctx) へ載せ替え
- createApp相当の層を実行環境ごとに分ける(runtimes/express.js, runtimes/bun.js 案)
- MainRouter の改名
- ロゴ(漢字「鳥人」+ TORIHITO)、npm名・リポジトリ・ドメインの確保
