# parlaspeech
GPU heavy part for the newest iteration of ParlaSpeech efforts


# VAD

The old API did not work for me, so I use an updated variant. This requires my access token, which is hidden in my secrets file.

# Logits

## Wav2Vec2 model eval

HF Hub has 4 wav2vec2 models for BG. I evaluated all of them on [test audio](testaudio.mp3):

```
Model:  DrishtiSharma/wav2vec2-large-xls-r-300m-bg-d2
ваджай ми народне представите лви… завет местата си процедура гсн цоневжая ми гостди председателтова къйто ни престои да гласуваме… изкючително важна европейска норма с поряднас… затоятеилна препоръки и на велицанската комисия на европейските институцие… предвед на дебата… аз предлагам — прекретивание на заседанието  предпълна зала утре… а и пред със достатъчно отговорност и ка мевропейска българя да гласувви тога… благодаря ви има ли противно предложение не виждам… моля ви лежимна гласуване за тазий…… … процедура прекретте гласуанятакубичите посвечтирезултат… гласува ви осемдесети четири народни престаиили засшесетишеспрот в девет весздържецедее — прекраяме заседанието отривдесовозова

vadzhay mi narodne predstavite lvi… zavet mestata si protsedura gsn tsonevzhaya mi gostdi predsedateltova kayto ni prestoi da glasuvame… izkyuchitelno vazhna evropeyska norma s poryadnas… zatoyateilna preporaki i na velitsanskata komisiya na evropeyskite institutsie… predved na debata… az predlagam — prekretivanie na zasedanieto  predpalna zala utre… a i pred sas dostatachno otgovornost i ka mevropeyska balgarya da glasuvvi toga… blagodarya vi ima li protivno predlozhenie ne vizhdam… molya vi lezhimna glasuvane za taziy…… … protsedura prekrette glasuanyatakubichite posvechtirezultat… glasuva vi osemdeseti chetiri narodni prestaiili zasshesetishesprot v devet veszdarzhetsedee — prekrayame zasedanieto otrivdesovozova


Model:  DrishtiSharma/wav2vec2-large-xls-r-300m-bg-v1
вжем народне престайтеви заеемете местата сипроцедра гаспон цоневжами гостим пресеателтакато непрестоида глосулме изкучтелно важна явропесканормас пораас закоато има препорък и навеницанската комсе неврпескитинстетуципрадвът на дебата аз предлагам кракратяане на заседането  предполназала утре аиря създустаташна отгворности камеврпеска българя да глсолнетогаблогадории имаме пртивнопредложение невиждам  молявирежим на гласоанезатазипруцдура прекратета гласуланатокобиче те посчетрязултатгласула иосъмдесети четири на родни престайтели засше сти е с проти в девят вздържецадеят  прекретяме заседанят отреб деосда

vzhem narodne prestaytevi zaeemete mestata siprotsedra gaspon tsonevzhami gostim preseateltakato neprestoida glosulme izkuchtelno vazhna yavropeskanormas poraas zakoato ima preporak i navenitsanskata komse nevrpeskitinstetutsipradvat na debata az predlagam krakratyaane na zasedaneto  predpolnazala utre airya sazdustatashna otgvornosti kamevrpeska balgarya da glsolnetogablogadorii imame prtivnopredlozhenie nevizhdam  molyavirezhim na glasoanezataziprutsdura prekrateta glasulanatokobiche te poschetryazultatglasula iosamdeseti chetiri na rodni prestayteli zasshe sti e s proti v devyat vzdarzhetsadeyat  prekretyame zasedanyat otreb deosda


Model:  anuragshas/wav2vec2-large-xls-r-300m-bg
оважами народне преставйте ви замте местата си процедура гпдн цоневжайми госпоин председател това което ни престои да гласуваме изключително важна европейска норма според нас закоято има препоръки и на веницианската комисея на европейските институци предвът на дебата аз предлагам прекртяване на заседанието е предпълна зала утре а и пред създостатъчна отговорности къмевропейска българя да гласъвме тога благодаря ви имаме противно предложение не виждам моля ви режим на гласуване за тази роцедура прекретете гласуванетокобичте по сечетире зултатгласував осъмдесети четири народни престайе ви дасшейетишеспротив девет васдържеце девет прекретяме заседанието утрев десесеседа

ovazhami narodne prestavyte vi zamte mestata si protsedura gpdn tsonevzhaymi gospoin predsedatel tova koeto ni prestoi da glasuvame izklyuchitelno vazhna evropeyska norma spored nas zakoyato ima preporaki i na venitsianskata komiseya na evropeyskite institutsi predvat na debata az predlagam prekrtyavane na zasedanieto e predpalna zala utre a i pred sazdostatachna otgovornosti kamevropeyska balgarya da glasavme toga blagodarya vi imame protivno predlozhenie ne vizhdam molya vi rezhim na glasuvane za tazi rotsedura prekretete glasuvanetokobichte po sechetire zultatglasuvav osamdeseti chetiri narodni prestaye vi dassheyetishesprotiv devet vasdarzhetse devet prekretyame zasedanieto utrev deseseseda


Model:  infinitejoy/wav2vec2-large-xls-r-300m-bulgarian
оважай минародне престаители завете местата си процедор гатинцоневжа ми госпои прецедателтоа кото не престои да гасовее изключително важна европеска нормаспоранас закоато има преорък и на велицанскита комесе н вропейските нстетуципредвет на дебата аз предлагам прекретяваня на заседаниято е предпълна залаутре а и предсъздустатшно отговорности към еврпейска балгаря да гаоветога бладоряли имале противно предожение не виждам  моляви режим на гласлана затазий пруцедорпрекретете гласилането кобичте осочетрезутатгласилалиосъмдесети четири народни пресайели заш сти шес проти в девя въздржцедеет преряме з седането утрев десосла

ovazhay minarodne prestaiteli zavete mestata si protsedor gatintsonevzha mi gospoi pretsedateltoa koto ne prestoi da gasovee izklyuchitelno vazhna evropeska normasporanas zakoato ima preorak i na velitsanskita komese n vropeyskite nstetutsipredvet na debata az predlagam prekretyavanya na zasedaniyato e predpalna zalautre a i predsazdustatshno otgovornosti kam evrpeyska balgarya da gaovetoga bladoryali imale protivno predozhenie ne vizhdam  molyavi rezhim na glaslana zataziy prutsedorprekretete glasilaneto kobichte osochetrezutatglasilaliosamdeseti chetiri narodni presayeli zash sti shes proti v devya vazdrzhtsedeet preryame z sedaneto utrev desosla
```