11��9�Ŵ�git�и��º�����64λGVIM��֧��Python3.2��Python2.7��Perl��TCL/TCӦ������ͦȫ���ˣ������ĵ�353��

�޸���һ��Դ�룬���ڽ��GVIM�ױߵ����⣬��Ϊ��ʹ�õ���ɫΪmolokai�����Ը�����ɫ�Ǻ�ɫ�ġ�

�޸� gui_w32.c  �� 1471 ��.
    wndclassw.hbrBackground = CreateSolidBrush(RGB(27, 29, 30));

����ʱbigvim.bat�е�����
    nmake -f Make_mvc.mak GUI=yes OLE=yes PERL=C:\Perl64 DYNAMIC_PERL=yes PERL_VER=514 PYTHON=C:\Python27 DYNAMIC_PYTHON=yes PYTHON_VER=27 PYTHON3=C:\Python32 DYNAMIC_PYTHON3=yes PYTHON3_VER=32  TCL=c:\tcl TCL_VER=85 DYNAMIC_TCL=yes %1 IME=yes CSCOPE=yes

vim73Ŀ¼�������˼���dll�ļ�

  - gvimext.dll���޸Ĺ���ģ����ܼ��ˣ���ѡ�񵥸��ļ�ʱ�Ҽ��˵�ֻ�����һ�� "Edit with VIM"����ѡ�����ļ�ͬʱ������"Diff with VIM"��ͬʱ������ͼ�ꡣ
  - gvimfullscreen.dll�Ǹ��൱ȫ�Ķ���������VIMȫ����͸����������ǰ���ܣ���vimrc�������������ʹ��

  	" {{{ Winƽ̨�´���ȫ����� gvimfullscreen.dll
  	" Alt + Enter ȫ���л�
  	" Shift + t ���ʹ���͸����
  	" Shift + y �Ӵ󴰿�͸����
  	" Shift + r �л�Vim�Ƿ�������ǰ����ʾ
  	if has('gui_running') && has('gui_win32') && has('libcall')
  		let g:MyVimLib = 'gvimfullscreen.dll'
  		function! ToggleFullScreen()
  			"let s:IsFullScreen = libcallnr("gvimfullscreen.dll", 'ToggleFullScreen', 0)
  			"let s:IsFullScreen = libcallnr("gvimfullscreen.dll", 'ToggleFullScreen', 27 + 29*256 + 30*256*256)
  			call libcall(g:MyVimLib, 'ToggleFullScreen', 27 + 29*256 + 30*256*256)
  		endfunction
  		"ӳ�� Alt+Enter �л�ȫ��vim
  		map <a-enter> <esc>:call ToggleFullScreen()<cr>
  		"Vim������ʱ���Զ�����InitVim ��ȥ��Vim�İ�ɫ�߿�
  		autocmd GUIEnter * call libcallnr(g:MyVimLib, 'InitVim', 0)
  
  		let g:VimAlpha = 240
  		function! SetAlpha(alpha)
  			let g:VimAlpha = g:VimAlpha + a:alpha
  			if g:VimAlpha < 180
  				let g:VimAlpha = 180
  			endif
  			if g:VimAlpha > 255
  				let g:VimAlpha = 255
  			endif
  			call libcall(g:MyVimLib, 'SetAlpha', g:VimAlpha)
  		endfunction
  		"����Vim����Ĳ�͸����
  		nmap <s-t> <esc>:call SetAlpha(10)<cr>
  		"����Vim�����͸����
  		nmap <s-y> <esc>:call SetAlpha(-10)<cr>
  
  		let g:VimTopMost = 0
  		function! SwitchVimTopMostMode()
  			if g:VimTopMost == 0
  				let g:VimTopMost = 1
  			else
  				let g:VimTopMost = 0
  			endif
  			call libcall(g:MyVimLib, 'EnableTopMost', g:VimTopMost)
  		endfunction
  		"�л�Vim�Ƿ�����ǰ����ʾ
  		nmap <s-r> <esc>:call SwitchVimTopMostMode()<cr>
  	endif
  	" }}}


