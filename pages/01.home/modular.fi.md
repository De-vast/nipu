---
title: 'Nikon sivut'
content:
    items: '@self.modular'
    order:
        by: default
        dir: asc
        custom:
            - _intro
            - _who-i-am
            - _what-i-do
            - _my-work
            - _contact
form:
    action: /home
    name: contact-form
    fields:
        -
            name: name
            label: Name
            placeholder: Nimesi
            type: text
            validate:
                required: true
        -
            name: email
            label: Email
            placeholder: Sähköpostiosoitteesi
            type: email
            validate:
                required: true
        -
            name: message
            label: Message
            placeholder: 'Kysymyksiä? Risuja tai ruusuja?'
            type: textarea
            rows: 6
            validate:
                required: true
    buttons:
        -
            type: submit
            value: 'Lähetä viesti'
    process:
        -
            email:
                from: '{{ config.plugins.email.from }}'
                to: ['{{ config.plugins.email.from }}']
                subject: '[Contact] Viesti - {{ form.value.name|e }}'
                body: '{% include ''forms/data.html.twig'' %}'
        -
            save:
                fileprefix: contact-
                dateformat: Ymd-His-u
                extension: txt
                body: '{% include ''forms/data.txt.twig'' %}'
        -
            display: thank-you
---

