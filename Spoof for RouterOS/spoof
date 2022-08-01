:local content [/file get [/file find name=flash/stable.txt] contents] ;
:local contentLen [:len $content];

:local lineEnd 0;
:local line "";
:local lastEnd 0;
:local varnet "down";
:local inwlan "wlan1";

:while ($lineEnd < $contentLen) do={
:set lineEnd [:find $content "\n" $lastEnd];
:if ([:len $lineEnd] = 0) do={
:set lineEnd $contentLen;
}
:set line [:pick $content $lastEnd $lineEnd];
:set lastEnd ($lineEnd + 1);
:if ($line != "\n") do={
:delay 10
:local net [/tool netwatch get 0 value-name=status];
:if ($net = $varnet) do={ 
:log warning "Netwatch $net | New Mac $line";
/interface wireless set $inwlan mac-address=$line
/ip dhcp-client release $inwlan
} else={ 
:log warning "Netwatch $net | internet connected";
 /quit }
}
}
/system script run spoof
