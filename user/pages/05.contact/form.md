---
title: 'Contact - Devis'
process:
    markdown: true
    twig: true
form:
    name: contact-form
    fields:
        -
            name: name
            label: 'Nom / Société'
            placeholder: 'Entrer votre nom / le nom de la société'
            type: text
            size: large
            validate:
                required: true
        -
            name: email
            label: 'Adresse email'
            placeholder: 'Entrer votre adresse email '
            size: medium
            type: email
            validate:
                required: true
        -
            name: type
            label: Type
            type: toggle
            options:
                - 'Un particulier'
                - 'Une entreprise privée'
                - 'Une commune'
                - Autre
            validate:
                required: true
        -
            name: message
            label: Demande
            placeholder: 'Indiquer votre demande'
            type: text
            validate:
                required: true
    buttons:
        -
            type: submit
            value: Envoyer
    process:
        -
            reset: true
            email:
                from: '{{ config.plugins.email.from }}'
                to:
                    - '{{ config.plugins.email.to }}'
                    - '{{ form.value.email }}'
                subject: '[Feedback] {{ form.value.name|e }}'
                body: '{% include ''forms/data.html.twig'' %}'
        -
            save:
                fileprefix: feedback-
                dateformat: Ymd-His-u
                extension: txt
                body: '{% include ''forms/data.txt.twig'' %}'
        -
            message: 'Merci pour votre mesage {{ form.value.name|e }}!'
        -
            display: thanks
---

<center><h1>Contact - Devis en ligne</h1></center>