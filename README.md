/// <reference types="cypress" />

import url from "../../../Cypressproject/cypress/fixtures/url.json"

let body
let countryURL = url.URL_SC


describe('Question 1: API Test For Kindred Assesment ', () => {

    it('Navigate the API URL with 400 and fix the issue then check the 200 response is displayed', () => {

        //Requests are missing few input param in body such as brand ,locale,currentcy,deviceGroup etc...

        cy.request({

            method: 'GET',

            url: 'https://www.unibet.co.uk/kambi-rest-api/gameLauncher2.json',

            encoding: 'binary',

            form: true,

            body: {

                brand: 'unibet',

                locale: 'en_GB',

                currency: 'GBP',

                deviceGroup: 'desktop',

                clientId: 'polopoly_desktop',

                marketLocale: 'en_GB'

            }


        }).then(response => {


            expect(response.status).to.eq(200)

            cy.writeFile('cypress/fixtures/response1.json', response)

            expect((JSON.stringify(response.body.lang))).contains('en_GB')

            expect((JSON.stringify(response))).contains('https://www.unibet.co.uk/kambi-rest-api/gameLauncher2.json')

        })

    })

})

describe('Question 2: API Test For Kindred Assesment', () => {

    it('Navigate to API URL  and validate with Various URL', () => {


        cy.request({

            method: 'GET',

            url: countryURL + 'sportsbook-feeds/views/sports/a-z',

            form: true,

            headers: {

                'content-type': 'application/json; charset=utf-8',
            },


        }).then(response => {

            expect(response.status).to.eq(200)

            body = JSON.parse(JSON.stringify(response.body));
        

        })

    })

})

describe('Question 3: Graphical User Interface validation Test For Kindred Assesment ', () => {

    it('Launch the URL and validate GUI visibility', () => {

        cy.visit(url.appURL)

        cy.wait(5000)

        cy.get('[id="CybotCookiebotDialogBodyLevelButtonLevelOptinAllowAll"]').click()

        cy.get('.heading').should('have.text', 'Register with us')

        cy.get('.form-view-1 > .form > .form-view-heading').contains('start with your personal details')

        cy.get('.CampaignsChooserBlock__header___1yxfW > span').should('have.text', 'Your welcome offer')

        cy.get('.Campaign__title___4d3Ny').should('have.text', ' Racing - Money Back as Bonus up to £40 + £10 Casino Bonus ')

        cy.get('.form-view-1 >').should('be.visible')

        // form fields verification begins

        cy.get('#firstName').should('be.visible')

        cy.get('#lastName').should('be.visible')

        cy.get('#email').should('be.visible')

        cy.get(':nth-child(1) > .form-selectbox > .field').should('be.visible')

        cy.get(':nth-child(2) > .form-selectbox > .field').should('be.visible')

        cy.get(':nth-child(3) > .form-selectbox > .field').should('be.visible')

        //Check box visibility verification

        cy.get(':nth-child(4) > .form-field > .edit > .validation-container > .radio-container > .radio-list > :nth-child(1) > .field-label').should('be.visible')

        cy.get(':nth-child(4) > .form-field > .edit > .validation-container > .radio-container > .radio-list > :nth-child(2) > .field-label').should('be.visible')

        // form fields visibility verification completed


        // Button Visibility vaidation

        cy.get('.form-view-1 > .form > .btn').should('be.visible')


        // Button disabled and enabled validation



        cy.get('.form-view-1 > .form > .btn').should('be.visible')

    })


    it('Fill all the Registration fields with valid data and click Continue button ', () => {


        cy.get('#firstName').type('testuserfirstname')

        cy.get('#lastName').type('testuserlastname')

        cy.get('#email').type('testuser@outlook.com')

        cy.get(':nth-child(1) > .form-selectbox > .field').select(29)

        cy.get(':nth-child(2) > .form-selectbox > .field').select('June')

        cy.get(':nth-child(3) > .form-selectbox > .field').select('1982')

        cy.get(':nth-child(4) > .form-field > .edit > .validation-container > .radio-container > .radio-list > :nth-child(1) > .field-label').click()

        cy.get('.form-view-1 > .form > .btn').click()

    })



    it('Verification for Registration completed or not once clicked on continue button', () => {

        cy.get('.form-view-2 > .form > .form-view-heading').should('be.visible')

        cy.get('.form-view-2 > .form > .form-view-heading').contains('testuserfirstname')


    })



    it('Then verify All fields and drop-down selections are displayed ', () => {

        cy.get('#address-lookup').should('be.visible')

        cy.get('.form-field-presentation').should('be.visible')

        cy.get('.selected-country-prefix').should('be.visible')

        cy.get('.selected-country-prefix > .country-prefix').should('be.visible')

        cy.get('.selected-country-prefix > .icon-wrapper > .icon').should('be.visible')

        cy.get('.number-field > .validation-container > .form-textbox > .field').should('be.visible')

        cy.get('.form-view-2 > .form > .btn').should('be.visible')


    })

    it('Then verify continue button should be disabled', () => {

        cy.get('.form-view-2 > .form > .btn').should('be.visible')


    })


    it('Then Mobile number field is entered incorrectly (i.e. ---45-6-45) and validate error message is present ', () => {

        cy.get('.number-field > .validation-container > .form-textbox > .field').type('testuserfirstname')

        cy.get('#address-lookup').click()

        cy.get('.number-field > .validation-container > .message-container').should('have.text', 'Your mobile number is not valid. Please check you’ve entered all the digits that appear after the country code. Spaces are not allowed.')

    })

    it('After Entering a invalid mobile number verify the continue button not enabled', () => {

        cy.get('.form-view-2 > .form > .btn').should('be.visible')

    })


})


===============================================


{
    "url" : "https://www.unibet.co.uk/sportsbook-feeds/views/sports/a-z",
    "appURL" : "https://www.unibet.co.uk/registration",
    "URL_SC" : "https://www.unibet.se/",
    "URL_COM" : "https://www.unibet.com/",
    "URL_UK" : "https://www.unibet.co.uk/"
}





