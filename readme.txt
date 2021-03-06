※ソースコードのコンパイルについて

作成環境は Cygwin + PSPSDK (revision 2318) です。
おそらくそれ以前の環境でもコンパイルは可能だと思われますが、出来る限り
最新の環境を使っていただくのが望ましいと思います。

コンパイルの際は、Makefileの先頭にあるConfigurationの項目を編集することで
コンパイルの対象を設定します。各項目の先頭に#をつけてコメントアウトする
ことで無効に、#を削除することで有効になります。以下詳細です。


・コンパイルの設定

BUILD_CPS1PSP = 1      CPS1PSPのコンパイルを行います。

BUILD_CPS2PSP = 1      CPS2PSPのコンパイルを行います。

BUILD_MVSPSP = 1       MVSPSPのコンパイルを行います。

BUILD_NCDZPSP = 1      NCDZPSPのコンパイルを行います。

PSP_SLIM = 1           PSP-2000 + CFW3.71 M33以降用のユーザーモードで実行
                       するバイナリをコンパイルします。

KERNEL_MODE = 1        FW1.5のカーネルモードで実行するバイナリを作成します。

SAVE_STATE = 1         ステートセーブ/ロード機能を組み込みます。

ADHOC = 1              AdHoc通信対戦機能をくみこみます。(KERNEL_MODEを有効に
                       している場合のみ)

COMMAND_LIST = 1       コマンドリスト機能を組み込みます。

JAPANESE_UI = 1        日本語ユーザインタフェース版を作成します。

UI_32BPP = 1           ユーザインタフェースの描画を32bitカラーで行います。
                       壁紙も使用可能になりますが、NCDZPSP以外ではメモリの
                       消費を抑えるためにもこのフラグは無効にしておくほうが
                       良いです。

RELEASE = 1            有効にするとREREASE = 1を、無効にするとRELEASE = 0を
                       コンパイルの定数として設定します。
                       ソース中で #if RELEASE 〜 #endif のように使用します。
                       現状は有効にするとbootleg版のゲームが起動できるように
                       なります。

・バージョンの設定

VERSION_MAJOR = 2      メジャーバージョンは大規模な更新を行った場合に変更を行います。

VERSION_MINOR = 2      マイナーバージョンは小規模な更新を行った場合に変更を行います。
                       また、偶数の場合は安定版、奇数の場合は開発版となります。
                       したがって、ver.1.0の次はver.1.2がリリースバージョンになります。

VERSION_BUILD = 0      ビルド番号は細かいバグ修正を行った場合に変更を行います。

----------------------------------------------------------------------------------------

※最適化オプション

コンパイラの最適化によって、動作が不安定になる場合があるようです。
-O2でコンパイルしておかしい場合は、-O3でコンパイルして試してみてください。

----------------------------------------------------------------------------------------

※ver.2.2.1での変更点

・file_open()で変な処理を行っていたので修正。


※ver.2.2.0での変更点

ソースの構造自体は特に大きな変更は行っていません。
動作確認が甘いので、うまく動作しない場合は2.0.6のソースコードと変更点を
比較して修正を行っていただけると助かります。

・CPS2PSPとMVSPSPをPSP-2000の拡張されたメモリに対応。
  CPS2PSPはキャッシュ不要で動作するようになります。
  MVSPSPは従来どおりキャッシュを作成する必要があります。
  (PSP_SLIMフラグを有効にしてコンパイルすること)

・MAME 0.119までに追加されたROMセットに対応。

・MAME Plus!で対応しているbootlegセットを追加。(REREASEフラグ無効でコンパイルすること)

・ver.2.0.6でいくつかの細かいバグがあったので修正。

・PSPSDKを最新版に更新したところコンパイル不能になっていたため、型定義の表記を
  従来のu8、u16等からMAMEのUINT8、UINT16等の表記に変更。
