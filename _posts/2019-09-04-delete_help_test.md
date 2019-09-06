RSpecでdelete_helpのテストを行う際に変更した点

my_help_controll.rbのdelete_helpメソッドを書き換えた

<br>
変更前

  > ``` {.example}
　　def delete_help(file)
　　  file = File.join(@local_help_dir,file+'.org')
　　  print "Are you sure to delete "+file.blue+"?[Ynq] ".red
　　  case STDIN.gets.chomp
　　  when 'Y'
　　    begin
　　      FileUtils.rm(file,:verbose=>true)
　　    rescue => error
　　      puts error.to_s.red
　　    end
　　   when 'n', 'q' ; exit
　　   end
　　 end
  >```

<br>
変更後

  > ``` {.example}
　　def delete_help(file)
　　  file = File.join(@local_help_dir,file+'.org')
　　  print "Are you sure to delete "+file.blue+"?[Ynq] ".red
　　  case STDIN.gets.chomp
　　  when 'Y'
　　	begin
　　      FileUtils.rm(file,:verbose=>true)
　　      return 1
　　	rescue => error
　　      puts error.to_s.red
　        return 2
　	end
　    when 'n', 'q' ; return 0
　    end
　  end
  > ```

理由

変更前のものでテストを行う場合，ユーザー入力でn,q を入力した際にexitと返される．その時点でRubyのプロセスが終了してしまうためテストを続行できない．そのため書き換えた.
return を用い，それぞれのケースごとの戻り値を見ることでテストが正しいか判断できる．

