+++
draft = false
date = 2024-08-17T11:25:17+00:00
title = "Tips till en 18-åring"
description = ""
slug = ""
authors = ['zev']
tags = []
categories = []
externalLink = ""
series = []
+++

This is in response to [Säkerhetspodcasten](https://sakerhetspodcasten.se/) episode [264](https://sakerhetspodcasten.se/posts/sakerhetspodcasten_264_tips_till_en_18_aring/), about what tips you would have given yourself as an 18-year-old in the context of later ending up in the cybersecurity field. This is an episode I asked for, so I guess I should also pitch in. As the podcast is in Swedish, this blog post will also be in Swedish, but you could use your tool of choice to translate if you find it interesting.

Tack för ett fint avsnitt i vanlig ordning. Jag håller i stort med om att vad man gör inte spelar så stor roll. Att bara göra vad man tycker är roligt är bra för motivation, men man kommer köra fast och då är det lite en kulle att komma över innan det blir kul igen. Då är det lätt att det bara blir spel eller öl istället (så är det väl för övrigt fortfarande?). En sak högskolan lärde mig är att leva i den ständiga känslan av att inte kunna något men trots detta kämpa vidare, stuck in active som de så fint kallade det. Det där att jag inte hade råd att bo kvar om jag inte klarade mina kurser var en bra motivation. Det tog något år av ångest innan jag blickade tillbaka och insåg att det jag inte förstod då, nu var rätt självklart och att det tar tid för kompetens att faktiskt landa. Även om man kan alla glosor och kan rabbla upp hur tekniker fungerar. Man måste ha tålamod. Därför tror jag det är bra att ha lite mål och inte ge upp, impostor syndrome är också en grej. Här är några förslag på projekt att ge sig an:

- Skruva isär alla saker som gått sönder och se om du fattar vad som gått sönder och varför. Det hjälper dig felsöka. En trasig kaffebryggare är ändå trasig så det gör inget om du inte får ihop den igen.
- Bygg en hemsida via goHugo och ge inte upp innan den är produktionssatt med ett let's encrypt-cert och koden är synkad till Github. Det kräver att du tar dig runt i Linux, konfar lite nginx eller apache, laddar ner lite mjukvara från Github, googlar lite på git och försöker förstå vad som gör vad i ditt valda tema. Eventuellt kräver det lite port forwarding i din router också. Det är ett större projekt än man kanske först tänker.
- Sätt upp något self-host projekt. Nextcloud, Vikunja, något NAS, Home Assistant, Immich eller liknande. Detta går att göra på din egen dator, men är eventuellt roligare att göra på någon VPS (det kostar dock ofta pengar). Att lära sig hantera servrar är mycket användbart.
- På ovan punkt, lär dig något om docker eller kubernetes.
- Skriv något script som gör vad som helst. Ge inte upp innan det fungerar och ligger på Github, ha lagom ambitionsnivå. Python, bash eller powershell är bra scriptspråk att börja med.
- Lagra någon data i en databas. Se om du kan mata in data programatiskt. Grist tror jag är ett bra steg om du vill se vad som händer grafiskt.
- Sätt upp en Proxmox-server på någon dator du kanske har över, har du inte det, skicka ett fint mail till lite bolag, gamla laptops brukar det finnas gott om så länge du kan tänka dig att köpa en egen hårddisk. 

Vad är då poängen med allt detta? Du kommer oavsett roll behöva göra massor av felsökning. Det spelar ingen roll om du blir utvecklare, pentestare, sysadmin, IT-arkitekt, nätverkstekniker eller något annat inom IT. Ovan projekt kommer tvinga dig in i felsökning. Dessutom är det mesta generella kunskaper som du kommer ha nytta av oavsett var du hamnar sen.

Är man väldigt inne på IT-säk och tycker att det jag skriver ovan låter för generellt eller kanske till och med är något man redan gör kommer här lite mer specifika tips:

- Köp eller önska dig en prenumeration på TryHackMe och gör det du tycker är kul.
- Hacka i CTF, säkerhets-SM och PicoCTF är bra platser att börja på.
- Mata i dig dragningar och poddar, nästan alla konferenser lägger upp saker på YouTube, börja anteckna.
- Gå en praktisk utbildning, högskoleingenjör eller YH om du är praktiskt lagd, annars vad som helst inom teknik. Att gå på högskola gör också att du skaffar dig kontakter, det kan vara mycket användbart senare i livet. Om inte annat är det rätt vanligt att folk träffar en del av sina närmaste vänner under studietiden.
- Skaffa ett jobb inom support, det kommer tvinga dig att felsöka massor och ställa rätt frågor. Att lära sig bryta ner ett problem till ja- och nej-frågor är mycket användbart.
- Gå på konferenser, många har studentpriser, ibland kan man prata med någon snäll sponsor som tycker att nytt blod är bra, eller kolla om du kan hjälpa till och komma in på det viset. Att hänga på konferenser är lärorikt och inspirerande, glöm bara inte att du inte är ensam om att inte förstå hälften av allt folk säger på scen, många i publiken är minst lika undrande, det var det där med impostor syndrome igen.

Jag har nu gett massor av exempel på saker att göra, det är inte en checklista. Ingen av oss kan allt, det är omöjligt. Välj en sak, gör den, när du känner dig klar ta kanske en annan. Tänk inte på berget av kunskap utan njut av stigen, och specialisera dig inte för tidigt. Gemensamt för alla du ser upp till är att de vid något tillfälle inte heller kunde något. Idag är inte bristen på information problemet utan istället hur du ska välja vilken information som är värd att ta till dig. Byt ut orden "jag måste" mot "jag vill" och gör dig beredd på att det är ett marathon och inte en sprint.

Ska du bara ta med dig något från det här inlägget, lär dig felsöka och va inte rädd att misslyckas.