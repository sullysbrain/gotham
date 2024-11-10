

function otherbats {
	grep "gotham" /etc/hosts | awk '{print $2}' | grep -v $(hostname)
}

function gothamcmd {
	for bat in $(otherbats); do ssh $bat -p 49242 "$@"; done
	$@
}

function gothamreboot {
  gothamcmd sudo shutdown -r now
}

function gothamshutdown {
  gothamcmd sudo shutdown now
}

function gothamscp {
  for bat in $(otherbats); do
    cat $1 | ssh $bat -p 49242 "sudo tee $1" > /dev/null 2>&1
  done
}


