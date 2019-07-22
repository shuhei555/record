- fizzbuzzを真似てコマンドラインからhelp,version,roman_numeralの解を出力するようにした．bundle exec exe/test -h, bundle exec exe/test to_roman num, bundle exec exe/test version

- 上記のテストをarubaを使い作成

  to be_successfully_executed
  status 0 で終了していることを確認
  not_to be_successfully_executed
  status 0 以外で終了していることを確認
  to have_output(contents)	
  出力が contents であることを確認。正規表現も使用可能


