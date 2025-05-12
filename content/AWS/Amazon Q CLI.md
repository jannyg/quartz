Jeg har tidligere kun testet Amazon Q kort i AWS Console da det ble lansert første gangen, men da  [Amazon Q Developer](https://aws.amazon.com/q/developer/) lanserte en ny og forbedret [CLI-agent](https://aws.amazon.com/about-aws/whats-new/2025/03/amazon-q-developer-cli-agent-command-line/) for kommandolinjen, bestemte jeg meg for å gi det en ny sjanse.

Den forbedrede CLI-agenten er en intelligent hjelper i terminalen som bruker AI for å gjøre utvikleropplevelsen med kommandolinjeverktøy både enklere og mer effektiv.

Med denne oppdateringen kan Amazon Q bruke informasjon fra utviklingsmiljøet ditt til å lese og skrive filer lokalt, hente data om AWS-ressurser og generere kode – alt direkte fra terminalen, uten at du trenger å bytte kontekst. Den kan foreslå kommandoer, rette feil, forklare output og gi kontekstuelle forslag – særlig i AWS CLI og relaterte verktøy.

# Introduksjon

I dette innlegget så tar jeg en nærmere titt på hvordan nye CLI-agenten fungerer i praksis. Jeg tester installasjon, oppsett og daglig bruk for å se om den kan være til nytte i hverdagen. 

Amazon Q CLI Støtter macOS, Linux og Windows, og installasjonsveiledning finnes på [GitHub](https://github.com/aws/amazon-q-developer-cli)]. For min del, som hovedsaklig benytter så macOS, så kunne den enkelt installeres med `brew install amazon-q`

## Autocomplete

En av de første tingene man legger merke til med Amazon Q er funksjonen *CLI-completions* som kan være veldig nyttig:

![[Pasted image 20250512094644.png]]

Det fungerer ikke bare for AWS CLI, men også med alle kommandolinjeverktøy:

![[Pasted image 20250512095050.png]]
Med en nyttig liste over alle parametere og korte beskrivelser for hver enkelt så kan man enkelt unngå skrivefeil eller behov for oppslag i dokumentasjonen (manpages). 

I bakgrunnen på siste bilde vises også eksempel på AI-genererte forslag direkte i shell.

# Translate

*Translate*-funksjonen lar deg skrive naturlig språk og få det oversatt til kommandoer:

![[Pasted image 20250512103319.png]]

## Chat

Med *Chat*-funksjonen så kan man også be Q om å utføre oppgaver lokalt, eller hente informasjon fra ditt AWS-miljø. Her er et enkelt eksempel hvor jeg ber Q om å fortelle meg hvor mange S3-bøtter jeg har, og ber den lage en liste med maskerte kontonummer:

![[Pasted image 20250512095909.png]]

Amazon Q benytter Amazon Bedrock og Claude 3.7 Sonnet som skal være godt egnet til å jobbe med kode. I dette eksempelet ber jeg Q lage en TypeScript-applikasjon som henter ut en liste over S3-bøtter og maskerer kontonummeret:

![[Pasted image 20250512101302.png]]
Legg merke til at man blir bedt om om å bekrefte bruken av verktøy/kommando underveis i løpet av sesjonen, eller om man ønsker å "stole på" agenten. Her mener jeg det er fornuftig å beholde kontrollen selv.

Den oppretter også `package.json` for avhengigheter og `tsconfig.json`:

![[Pasted image 20250512101644.png]]

Til slutt opprettes en *README* som forklarer hva applikasjonen gjør, og hvordan man installerer og bruker den:

![[Pasted image 20250512101923.png]]

Når alt er klart, får du en oppsummering av hva som er gjort, og korte instruksjoner om hvordan du tar det i bruk:

![[Pasted image 20250512102027.png]]

Etter å ha validert koden, tester jeg løsningen:

![[Pasted image 20250512102313.png]]
# Tilpasninger

### Profile og Context

Ved bruk av *profile* og *context*-funksjonene kan du definere hvilke filer som er relevante for sesjonen, og gi tilleggsinformasjon om prosjektet eller miljøet ditt. 

Eksempler:
- En "terraform"-profil med retningslinjer for infrastruktur som kode
- En "typescript"-profil med beste praksis og stilguider for TypeScript
## MCP

Amazon Q CLI støtter også _MCP_ (Modular Command Pipelines), som lar deg kommunisere med andre verktøy eller dele egendefinerte prompts med Q. Les mer om dette [her](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-mcp.html) 
# Oppsummering

Dette var en kort og uformell test av Amazon Q CLI, men førsteinntrykket er positivt. Verktøyet kan absolutt være nyttig for oss som bruker mye tid i terminalen.

Det er verdt å merke seg at hvis du ikke bruker *Amazon Q Professional tier*, må du aktivt slå av deling av innhold (opt-out) hvis du ikke ønsker å dele data med AWS. Les mer om det [her](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/opt-out-IDE.html).

Gi det gjerne en test – og del erfaringene dine eller nyttige tips underveis!