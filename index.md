Global Wordnet Formats
======================

The Global WordNet Association provides three formats for which WordNets can be
published and submitted to the ILI. These are as follows:

* [Lexical Markup Framework compatible XML](#xml)
* [JSON-LD using the lemon Vocabulary](#json)
* [lemon-based RDF](#rdf)

All of these formats are considered equivalent and a converter between them can 
be used at.

XML
---

The XML is specified by the following [DTD](WN-LMF-1.0.dtd). An example is 
given [here](https://github.com/globalwordnet/schemas/blob/master/example.xml):

The first three lines must always be as follows:

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE LexicalResource SYSTEM "http://globalwordnet.github.io/schemas/WN-LMF-1.0.dtd">
    <LexicalResource xmlns:dc="http://purl.org/dc/elements/1.1/">
    
A file may contain multiple WordNets in different languages:

The following information is required:

* id: A short name for the resource
* label: The full name for the resources
* language: Please follow BCP-47, i.e., use a two-letter code if 
             available else a three-letter code
* email: Please give a contact email address
* license: The license of your resource (please provide URL)
* version: A string identifying this version (preferably follow 
            major.minor format)
* url: A URL for your project homepage
* citation: The paper to cite for this resource

Extra properties may be included from Dublin core and in addition

* status: The status of the resource, e.g., "valid", "checked", "unchecked"
* confidenceScore: A numeric value between 0 and 1 giving the 
                    confidence in the correctness of the element.

        <Lexicon id="example-en"
                 label="Example wordnet (English)"
                 language="en" 
                 email="john@mccr.ae"
                 license="https://creativecommons.org/publicdomain/zero/1.0/"
                 version="1.0"
                 citation="CILI: the Collaborative Interlingual Index. Francis Bond, Piek Vossen, John P. McCrae and Christiane Fellbaum, Proceedings of the Global WordNet Conference 2016, (2016)."
                 url="http://globalwordnet.github.io/schemas/"
                 dc:publisher="Global Wordnet Association">
                 
Each word (lexical entry) must have a unique id:

            <LexicalEntry id="w1">

The part of speech values are as follows:

* n: Noun
* v: Verb
* a: Adjective
* r: Adverb
* s: Adjective Satellite
* z: Multiword expression (inc. phrase, idiom)
* c: Conjunction
* p: Adpoisiton (Preposition, postposition, etc.)
* x: Other (inc. particle, classifier, bound morphemes, determiners)
* u: Unknown

                <Lemma writtenForm="grandfather" partOfSpeech="n"/>
                <Sense id="example-10161911-n-1" synset="example-10161911-n"/>
            </LexicalEntry>
            <LexicalEntry id="w2">
                <Lemma writtenForm="paternal grandfather" partOfSpeech="n"/>
                <Sense id="example-1-n-1" synset="example-1-n">

The set of relations between senses is limited to the following

* antonym: An opposite and inherently incompatible word
* also: See also, a reference of weak meaning
* verb_group: Verb senses that similar in meaning and have been manually grouped together.
* participle: An adjective that is a participle form a verb
* pertainym: A relational adjective. Adjectives that are pertainyms are usually defined by such phrases as "of or pertaining to" and do not have antonyms. A pertainym can point to a noun or another pertainym
* derivation: A word that is derived from some other word
* domain_category: Indicates the category of this word
* domain_member_category: Indicates a word involved in this category described by this word
* domain_region: Indicates the region of this word
* domain_member_region: Indicates a word involved in the region described by this word
* domain_usage: Indicates the usage of this word
* domain_member_usage: Indicates a word involved in the usage described by this word

                    <SenseRelation relType="derivation" target="example-10161911-n-1"/>
                </Sense>
            </LexicalEntry>
            <LexicalEntry id="w3">
                <Lemma writtenForm="pay" partOfSpeech="v"/>
                
Syntactic Behaviour is given as in Princeton WordNet

                <SyntacticBehaviour subcategorizationFrame="Sam cannot %s Sue "/>
                <SyntacticBehaviour subcategorizationFrame="Sam and Sue %s"/>
                <SyntacticBehaviour subcategorizationFrame="The banks %s the check"/>
            </LexicalEntry>

If a synset is already mapped to the ILI please give the ID here

            <Synset id="example-10161911-n" ili="i90287">
                <Definition>
                    the father of your father or mother
                </Definition>
The set of relations between synsets is limited to the following:

* hypernym: A concept with a broader meaning
* hyponym: A concept with a narrower meaning
* instance_hypernym: The class of objects to which this instance belongs
* instance_hyponym: An individual instance of this class
* part_holonym: A larger whole that this concept is part of
* part_meronym: A part of this concept
* member_holonym: A group that this concept is a member of
* member_meronym: A member of this concept
* substance_holonym: Something where a constituent material is this concept
* substance_meronym: A constituent material of this concept
* entail: A verb X entails Y if X cannot be done unless Y is, or has been, done.
* cause: A verb that causes another
* similar: Similar, though not necessarily interchangeable
* also: See also, a reference of weak meaning
* attribute: A noun for which adjectives express values. The noun weight is an attribute, for which the adjectives light and heavy express values.
* verb_group: Verb senses that similar in meaning and have been manually grouped together.
* domain_category: Indicates the category of this word
* domain_member_category: Indicates a word involved in this category described by this word
* domain_region: Indicates the region of this word
* domain_member_region: Indicates a word involved in the region described by this word
* domain_usage: Indicates the usage of this word
* domain_member_usage: Indicates a word involved in the usage described by this word

                <SynsetRelation relType="hypernym" target="example-10162692-n"/>
            </Synset>

If you wish to define a new concept call the concept "in" (ILI New)

            <Synset id="example-1-n" ili="in">
                <Definition>A father's father; a paternal grandfather</Definition>

You can include metadata (such as source) at many points
The ILI Definition must be at least 20 characters or five words

                <ILIDefinition dc:source="https://en.wiktionary.org/wiki/farfar">
                    A father's father; a paternal grandfather
                </ILIDefinition>
            </Synset>

You must include all targets of relations

            <Synset id="example-10162692-n" ili="i90292"/>
        </Lexicon>
        <Lexicon id="example-sv"
                 label="Example wordnet (Swedish)"
                 language="sv" 
                 email="john@mccr.ae"
                 license="https://creativecommons.org/publicdomain/zero/1.0/"
                 version="1.0"
                 citation="CILI: the Collaborative Interlingual Index. Francis Bond, Piek Vossen, John P. McCrae and Christiane Fellbaum, Proceedings of the Global WordNet Conference 2016, (2016)."
                 url="http://globalwordnet.github.io/schemas/"
                 dc:publisher="Global Wordnet Association">

The list of lexical entries (words) in your wordnet

            <LexicalEntry id="w4">
                <Lemma writtenForm="farfar" partOfSpeech="n"/>

Synsets need not be language-specific but senses must be

                <Sense id="example-2-n-1" synset="example-1-n">
                    <SenseExample dc:source="Europarl Corpus">
                        Jag vill berätta för er att min farfar var svensk beredskapssoldat vid norska gränsen under andra världskriget, ett krig som Sverige stod utanför
                    </SenseExample>
                </Sense>
            </LexicalEntry>
        </Lexicon>
    </LexicalResource>


JSON
----

TTL
---
