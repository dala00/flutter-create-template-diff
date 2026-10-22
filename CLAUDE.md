# CLAUDE.md

## このリポジトリについて

`flutter create` で生成したまっさらなプロジェクトを Flutter のバージョンごとにコミットしていくリポジトリです。
Flutter をバージョンアップする際に、アプリケーション側（android/ios のテンプレートや設定ファイル等）で
何を変更すればよいかをコミット間の diff で確認するための参考用です。

- 生成物はほぼそのまま。手を入れるのはアプリケーションID（パッケージ名）程度
- README.md の `flutter create` コマンドの記載は手動で追記したもの（生成後も残す）
- `CLAUDE.md` はテンプレート外のファイル（生成後も残す）
- 対象プラットフォームは `ios,android` のみ

## コミット / タグの規約

- 1 バージョン = 1 コミット。コミットメッセージは Flutter のバージョン番号のみ（例: `3.35.7`）
- 同じコミットに同名のタグを付ける（例: `git tag 3.35.7`）
- バージョン間の差分確認: `git diff 3.32.0 3.35.7`

## 新しいバージョンを追加する手順

1. 対象バージョンの Flutter SDK を用意する（例: `git clone --depth 1 -b <version> https://github.com/flutter/flutter.git`）
2. 一時ディレクトリでプロジェクトを生成する

   ```bash
   flutter create --project-name flutter_create_template_diff --platforms "ios,android" flutter-create-template-diff
   ```

   - アプリケーションIDは Android `com.example.flutter_create_template_diff` / iOS `com.example.flutterCreateTemplateDiff`
     （直近の 3.35.7 に合わせる。古いバージョンでは `flutter_create_template_diff2` を使っていた時期がある）
3. リポジトリの `.git` 以外のテンプレート管理ファイルを削除し、生成物で置き換える
   （テンプレートから消えたファイルが残らないようにするため）
4. README.md の `flutter create` コマンド記載と CLAUDE.md を元に戻す
5. 生成時の `flutter pub get` で作られた `pubspec.lock` もコミットに含める
6. バージョン番号でコミットし、同名のタグを付ける
