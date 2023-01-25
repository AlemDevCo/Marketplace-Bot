## Marketplace Bot
##### Made by AlemDev#0001 and Riloo#8195
---
#### **Triggers**
---
##### /post
```
$resetUserVar[SelectMenu]
$newModal[modal;Post Info]
$addTextInput[modalInput1;paragraph;Post title;3;35;yes;;Post title]
$addTextInput[modalInput2;paragraph;Post description;2;499;yes;;Post description]
$addTextInput[modalInput3;paragraph;Payment with Robux / USD;2;2;yes;;Amount Robux / USD]
$addTextInput[modalInput4;paragraph;Twitter;2;50;no;;https://www.twitter.com/@username/]
$addTextInput[modalInput5;paragraph;Email;2;50;no;;name@domain.tld]
```

##### $onInteraction[modal]
```
$nomention
$ephemeral

Post preview
$title[$input[modalInput1]]
$description[$input[modalInput2]]
$addField[Payment;$input[modalInput3]]
$addField[Contact Info;
Discord: <@$userID[$username]>
Twitter: $input[modalInput4]
Email: $input[modalInput5]]
$color[00FF00]
$addButton[no;continue;Continue;primary;no;]

$setUserVar[submit; %{DOL}%title[$input[modalInput1]\]
%{DOL}%description[$input[modalInput2]\]
%{DOL}%addField[Payment\;$input[modalInput3]\]
%{DOL}%addField[Contact Info\;
Discord: <@%{DOL}%userID[%{DOL}%username\]>
Twitter: $input[modalInput4]
Email: $input[modalInput5]\]
%{DOL}%color[00FF00\] ]
```

##### $onInteraction
```
$if[$customID==continue]
$ephemeral
$nomention
$removeComponent[continue]
$eval[$getVar[SelectMenu]]
$endif

$if[$customID==channelMenu]
$if[$and[$checkContains[$getUserVar[SelectMenu];it]==true;$checkContains[$getUserVar[SelectMenu];Will]==true]]
 $ephemeral
 $nomention
 $removeComponent[categoryMenu]
 $removeComponent[channelMenu]
$removeComponent[post] 
$addButton[no;post;Submit;primary;no] 
 $else
 $ephemeral
$if[$message==hiring-option]

$elseif[$message==hireable-option]

$elseif[$message==selling-option]
$endif
$setUserVar[SelectMenu;$replaceText[$getUserVar[SelectMenu];will;Will;1]]
$endif
$if[$and[$checkContains[$getUserVar[SelectMenu];it]==true;$checkContains[$getUserVar[SelectMenu];Will]==true]]
 $ephemeral
 $nomention
 $removeComponent[categoryMenu]
 $removeComponent[channelMenu]
$removeComponent[post] 
$addButton[no;post;Submit;primary;no] 
$endif
$endif


$if[$customID==categoryMenu]
$if[$and[$checkContains[$getUserVar[SelectMenu];it]==true;$checkContains[$getUserVar[SelectMenu];Will]==true]]
 $ephemeral
 $nomention
 $removeComponent[categoryMenu]
 $removeComponent[channelMenu]
$removeComponent[post] 
$addButton[no;post;Submit;primary;no] 
 $else
 $ephemeral
 $if[$message==first-option]
 $nomention
   $setVar[category;building;$authorID]
  $elseif[$message==second-option]
  $nomention
   $setVar[category;scripting;$authorID]
  $elseif[$message==third-option]
  $nomention
   $setVar[category;GFX & 2D Art;$authorID]
  $elseif[$message==fourth-option]
  $nomention
   $setVar[category;Video Editing;$authorID]
  $elseif[$message==fifth-option]
  $nomention
   $setVar[category;Composor;$authorID]
  $elseif[$message==sixth-option]
  $nomention
   $setVar[category;UI (interface);$authorID]
  $elseif[$message==seventh-option]
  $nomention
   $setVar[category;Modeler;$authorID]
  $elseif[$message==eighth-option]
  $nomention
   $setVar[category;Other;$authorID]
 $endif
 $setUserVar[SelectMenu;$replaceText[$getUserVar[SelectMenu];It;it;1]]
$endif
$if[$and[$checkContains[$getUserVar[SelectMenu];it]==true;$checkContains[$getUserVar[SelectMenu];Will]==true]]
 $ephemeral
 $nomention
 $removeComponent[categoryMenu]
 $removeComponent[channelMenu]
$removeComponent[post] 
$addButton[no;post;Submit;primary;no] 
$endif
$endif
$if[$customID==post]
$var[channel;1064240085211566140]
$var[e;$sendEmbedMessage[$var[channel];;A request has been sent by _$username#$discriminator[]_.;;;;;;;;;;;yes]]
$useChannel[$var[channel]]
$addButton[no;Check;see;primary;;;$var[e]]
$endif
$if[$customID==Check]
$removeButtons
$deleteMessage[$var[channel];$var[e]]
$eval[$getUserVar[submit]]
$endif
```

---
#### **Variables**
---
##### category
No value.

##### SelectMenu
```
$newSelectMenu[categoryMenu;1;1;Category]
$addSelectMenuOption[categoryMenu;Building;first-option;It will be sent to that category.]
$addSelectMenuOption[categoryMenu;Scripting;second-option;It will be sent to that category.]
$addSelectMenuOption[categoryMenu;GFX & 2D Art;third-option;It will be sent to that category.]
$addSelectMenuOption[categoryMenu;Video Editing;fourth-option;It will be sent to that category.]
$addSelectMenuOption[categoryMenu;Composor;fifth-option;It will be sent to that category.]
$addSelectMenuOption[categoryMenu;UI (Interface);sixth-option;It will be sent to that category.]
$addSelectMenuOption[categoryMenu;Modeler;seventh-option;It will be sent to that category.]
$addSelectMenuOption[categoryMenu;Other;eighth-option;It will be sent to that category.]
$newSelectMenu[channelMenu;1;1;Channel]
$addSelectMenuOption[channelMenu;Hiring;hiring-option;Hiring a developer.]
$addSelectMenuOption[channelMenu;Hireable;hireable-option;Being hired as a developer.]
$addSelectMenuOption[channelMenu;Selling;selling-option;Selling stuff.]
```
