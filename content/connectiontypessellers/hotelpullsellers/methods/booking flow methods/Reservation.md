+++
title= "Reservation"
keywords= "hotel, data structure, reservation"
search= "Hotel - Data Structure - Reservation"
sidebar= "mydoc_sidebar"
permalink= "/docs/hotel/DSF/Reservation"
weight = 4
icon = "fa-thumbs-up"
+++



### Method Goals


This method aims to book an option.



### Request Format


The request format works the same way as *Valuation* but
with the list of passengers.



### Response Format


The result returns the booking locator (booking code), which could be the
supplier's own code or the one sent in request.



It also returns all the charges associated with the booking as well as its status.



### Remarks


**180000** milliseconds is the maximum amount of time permitted in our system before the connection
is closed. 



### ReservationRQ Example

In the request for this call it is necessary to use the object: "HotelBaseRQ". You can find the information in the section '[Common elements](/connectiontypessellers/hotelpullsellers/methods/common-elements/)'.

~~~xml
    <ReservationRQ>
        <ClientLocator>2537459</ClientLocator>
        <OnRequest>false</OnRequest>
        <Parameters>
            <Parameter key = "extra" value = "31"/>
        </Parameters>
        <DeltaPrice amount="10" percent="5" applyBoth="false"/>
        <StartDate>28/01/2014</StartDate>
        <EndDate>29/01/2014</EndDate>
        <MealPlanCode>D</MealPlanCode>
        <HotelCode>10</HotelCode>
        <Nationality>ES</Nationality>
        <Holder title = "Miss" name = "Test11" surname = "TestAp11" email = "hotelemail@email.com"/>
        <Price currency = "EUR" amount = "36.20" binding = "false" commission = "-1"/>
        <ResGuests> 
            <Guests>
                <Guest roomCandidateId = "1" paxId = "1">
                    <Title>Miss</Title>  
                    <GivenName>Test11</GivenName>
                    <SurName>TestAp11</SurName>
                </Guest>
                <Guest roomCandidateId = "1" paxId = "2">
                    <Title>Mr</Title>  
                    <GivenName>Test12</GivenName>
                    <SurName>TestAp12</SurName>
                </Guest>
            </Guests>
        </ResGuests>
        <PaymentType>MerchantPay</PaymentType>
        <CardInfo>
            <CardCode>VI</CardCode>
            <Number>4321432143214327</Number>
            <Holder>Test11 TestAp11</Holder>
            <ValidityDate>   
                <Month>06</Month>
                <Year>14</Year>
            </ValidityDate>
            <CVC>123</CVC>
        </CardInfo>
        <Rooms>
            <Room id = "4582" roomCandidateRefId = "1" code = "506" description = "Double Standard..">
            <Preferences>
                <Preference type = "Smoker"/>
                <Preference type = "NonSmoker"/>
                <Preference type = "ExtraBed"/>
                <Preference type = "Cradle"/>
                <Preference type = "DoubleBed"/>
                <Preference type = "TwinBeds"/>
            </Preferences>
            </Room>
            <Room id = "4583" roomCandidateRefId = "2" code = "507" description = "Twin Standard..">
            <Preferences>
                <Preference type = "Smoker"/>
                <Preference type = "NonSmoker"/>
                <Preference type = "ExtraBed"/>
                <Preference type = "Cradle"/>
                <Preference type = "DoubleBed"/>
                <Preference type = "TwinBeds"/>
            </Preferences>
            </Room>
        </Rooms>
        <RoomCandidates>
            <RoomCandidate id = "1">
                <Paxes>
                    <Pax age = "30" id = "1"/>
                    <Pax age = "30" id = "2"/>
                </Paxes>
            </RoomCandidate>
            <RoomCandidate id = "2">
                <Paxes>
                    <Pax age = "30" id = "1"/>
                    <Pax age = "30" id = "2"/>
                </Paxes>
            </RoomCandidate>
        </RoomCandidates>
        <Remarks>I want it a double bed.</Remarks>
        <Preferences>
            <Preference type = "ContiguosRooms"/>
            <Preference type = "Wedding"/>
            <Preference type = "LateArrival">14:00</Preference>
            <Preference type = "LateCheckOut"/>
            <Preference type = "GroundFloor"/>
            <Preference type = "TopFlor"/>
            <Preference type = "WithoutVoucher"/>
        </Preferences>
    </ReservationRQ>
~~~



**Important information about Number (Cardinal):**

Go to [Common-Elements](/connectiontypessellers/hotelpullsellers/methods/common-elements/#Important) for more information.



### ReservationRQ Description


| **Element**					| **Number**	| **Type**	| **Description**					|
| --------------------------------------------- | ------------- | ------------- | ----------------------------------------------------- |
| ReservationRQ 				| 1      	|		| Root node.						|
| ClientLocator 				| 1  		| String	| Booking ID in client's system.					|
| OnRequest     				| 1  		| Boolean	| Indicates if you want to receive the onrequest options in AvailRS, as long as the supplier returns it in this method (see [MetaData](/connectiontypessellers/hotelpullsellers/methods/staticcontent/metadata/) in order to verify if a supplier implements it).	|
| Parameters /   				| 0..1    	|		| List of parameters.	|
| Parameters /Parameter				| 1..n    	|		| Parameters for additional information that have been reported in ValuationRS.					|
| @key     					| 1  		| String	| Contains the keyword/Id to identify a parameter.	|
| @value   					| 1  		| String	| Contains the value of the parameter.			|
| DeltaPrice    				| 0..1    	|		| Indicates price variation permitted by the client (see [MetaData](/connectiontypessellers/hotelpullsellers/methods/staticcontent/metadata/) in order to verify if a supplier implements it). You can find more information with examples at [the bottom of this page](/connectiontypessellers/hotelpullsellers/methods/booking-flow-methods/reservation/#deltaprice-description).	|
| @amount  					| 0..1		| String	| Amount (in the currency returned into the option) that is accepted by the client to be higher than the valuation price. |
| @percent 					| 0..1		| String	| Percentage accepted by the client to be higher than the valuation price.	|
| @applyBoth					| 1  		| Boolean	| Indicates that the range between valuation price and the new price does not exceed the amount and/or porcentage indicated by the client.  |
| StartDate     				| 1  		| String 	| Start date to search rates. Format dd/MM/yyyy					|
| EndDate       				| 1  		| String	| End date to search rates. Format dd/MM/yyyy					|
| MealPlanCode  				| 1  		| String	| MealPlan code.					|
| HotelCode     				| 1  		| String	| Hotel code.						|
| Nationality   				| 1		| String	| Nationality of the Holder (use ISO3166_1_alfa_2 , see [MetaData](/connectiontypessellers/hotelpullsellers/methods/staticcontent/metadata/) in order to verify if a supplier implements it).  |
| Holder   				| 1		|		| Holder of the booking.  |
| @title   				| 1		| Enum	| Holder's title. Possible values: 0 = Mr, 1 = Mrs, 2 = Miss, 3 = Ms.   |
| @name   				| 1		|		| Holder's name.  |
| @surname   				| 1		|		| Holder's surname.  |
| @email   				| 0..1		|		| Holder's email.  |
| Price         				| 1      	|		| Total price of this valuation.			|
| @currency					| 1  		| String	| Currency code.					|
| @amount  					| 1  		| Decimal	| Option Amount.					|
| @binding 					| 1  		| Boolean	| Identifies if is the price is binding (When true the sale price returned **must** not be less than the price informed.  |
| @commission					| 1  		| Decimal	| Commission (-1 = not specified, 0 = net price, X = % of the commission applied to the amount.)	|
| ResGuests /    				| 1      	|		| List of passengers.				|
| ResGuests /Guests				| 1      	|		| Passengers.					|
| ResGuests /Guests/Guest			| 1..n    	|		| Detail of each passenger.	If the holder is also a passenger you need to add his/hers information in the gest list.			|
| @roomCandidateId				| 1  		| Integer	| Room candidate Identifier				|
| @paxId   					| 1  		| Integer	| Passenger id (starting at 1).				|
| ResGuests /Guests/Guest/Title		| 1 	 	| Enum	| Guest's title. Possible values: 0 = Mr, 1 = Mrs, 2 = Miss, 3 = Ms. 						|
| ResGuests /Guests/Guest/GivenName		| 1 	 	| String	| Guest's given name.						|
| ResGuests /Guests/Guest/SurName		| 1   		| String	| Guest's last name.						|
| PaymentType   				| 1  		| String	| Indicates the type of payment. It can be MerchantPay, LaterPay, CardBookingPay or CardCheckInPay. Payment types are explained in "Detailed description" section, in this same page.			|
| CardInfo /  				| 0..1  		|		| Credit card details.			|
| CardInfo /CardCode   				| 1  		| String	| Indicates the type of credit card. See types allowed at [Credit Card Types](/connectiontypessellers/hotelpullsellers/listsdata/#credit-cards)			|
| CardInfo /Number   				| 1  		| String	| Credit card number.			| 
| CardInfo /Holder   				| 1  		| String	| Credit card holder.			|
| CardInfo /ValidityDate   				| 1  		|		| 			|
| CardInfo /ValidityDate/Month   				| 1  		| String	| Expiration month (2 characters).			|
| CardInfo /ValidityDate/Year   				| 1  		| String	| Expiration year (2 characters).			|
| CardInfo /CVC   				| 1  		| String	| Credit card security code.			|
| CardInfo /isVCC   				| 1  		| Boolean	| Indicates if the card information provided is from a Virtual Credit Card or not.			|
| CardInfo /VirtualCreditCard   				| 0..1  		|		|  Extra information if the card is a virtual credit card.			|
| CardInfo /VirtualCreditCard/VCCActivationDate   				| 1  		| String	| Date from when the card can be charged. Format: DD/MM/YYYY.	|
| CardInfo /VirtualCreditCard/VCCDeactivationDate   				| 1  		| String	| Date from when the card will no longer be chargeable. Format: DD/MM/YYYY.	|
| CardInfo /VirtualCreditCard/VCCCurrentBalance   				| 1  		| String	| The amount which can be charged to the card.	|
| CardInfo /VirtualCreditCard/VCCCurrencyCode   				| 1  		| String	| The ISO currency code of the VCCCurrentBalance.	|
| CardInfo /ThreeDomainSecurity   				| 0..1  		|		| 3DS data and transaction results.			|
| CardInfo /ThreeDomainSecurity/ThreeDSVersion   | 1  		| String	| Three Domain Security version used.	|
| CardInfo /ThreeDomainSecurity/DSTransactionID  | 0..1 		| String	| Unique transaction identifier assigned by the Directory Server (DS) to identify a single transaction.	|
| CardInfo /ThreeDomainSecurity/XID              | 0..1 		| String	| Transaction identifier resulting from authentication processing.	|
| CardInfo /ThreeDomainSecurity/ECI              | 1  		| String	| Electronic Commerce Indicator. See values allowed at [ECI codes](/connectiontypessellers/hotelpullsellers/listsdata/#electronic-commerce-indicator-codes).|
| CardInfo /ThreeDomainSecurity/CAVV             | 0..1  		| String	| Cardholder Authentication Verification Value.	|
| CardInfo /ThreeDomainSecurity/PARes            | 0..1  		| String	| Payer Authentication Response.	|
| CardInfo /ThreeDomainSecurity/PAResStatus      | 0..1  		| String	| Payer Authentication Response status. See values allowed at [PARes Status](/connectiontypessellers/hotelpullsellers/listsdata/#pares-status).|
| CardInfo /ThreeDomainSecurity/PARes            | 0..1  		| String	| Payer Authentication Response.	|
| CardInfo /ThreeDomainSecurity/CardEnrolledStatus | 0..1  		| String	| Status of Authentication eligibility. See values allowed at [Card Enrollment Status](/connectiontypessellers/hotelpullsellers/listsdata/#card-enrollment-status).	|
| CardInfo /ThreeDomainSecurity/SignatureStatus  | 0..1  		| String	| Transaction Signature status.	See values allowed at [Signature Verification Status](/connectiontypessellers/hotelpullsellers/listsdata/#signature-verification-status).|
| CardInfo /ThreeDomainSecurity/MerchantName     | 0..1  		| String	| Merchant name.	|
| Rooms /         				| 1      	|		| Rooms within this option (room list).			|
| Rooms /Room    				| 1..n    	|		| Detail of room. 					|
| @id      					| 1  		| String	| Room identifier.				|
| @roomCandidateRefId				| 1  		| Integer	| Room candidate identifier.				|
| @code    					| 1  		| String	| Room code.						|
| @description					| 1  		| String	| Room description.					|
| Rooms /Preferences / 				| 0..1    	|		| Preference filters at room level. 					|
| Rooms /Preferences /Preference   				| 1..n    	|		| Each filter of preference and its values. 		|
| @type   				| 1    	|		| Type of preference allowed. See types allowed in **PreferenceType** further down this page   					|
| RoomCandidates /RoomCandidate			| 1..n    	|		| Room required.					|
| @id      					| 1  		| Integer	| Id of the requested room (starting at 1).		|
| RoomCandidates /RoomCandidate/Paxes /Pax	| 1..n    	|		| Pax required.						|
| @age     					| 1  		| Integer	| Passenger age on the day of check-in. 					|
| @id      					| 1  		| Integer	| Passenger id (starting at 1, this identifier is at room level). 			|
| Remarks       				| 0..1    	| 		| Any customer comments for the supplier to consider (see [MetaData](/connectiontypessellers/hotelpullsellers/methods/staticcontent/metadata/) in order to verify if a supplier implements it).	|
| Preferences /   				| 0..1    	|		| Preference filters at the option / general level. 					|
| Preferences /Preference   				| 1..n    	|		| Each filter of preference and its values. 		|
| @type   				| 1    	|		| Type of preference allowed. See types allowed in **PreferenceType** further down this page  					|
  


### ReservationRS Example

~~~xml
    <ReservationRS>
        <ProviderLocator>102</ProviderLocator>
        <PropertyReservationNumber>HCN8273</PropertyReservationNumber>
        <ResStatus>OK</ResStatus>
        <Price currency = "EUR" amount = "36.20" binding = "false" commission = "-1"/>
    </ReservationRS>
~~~



### ReservationRS Description


| **Element**					| **Number**	| **Type**	| **Description**					|
| --------------------------------------------- | ------------- | ------------- | ----------------------------------------------------- |
| ReservationRS					| 1       	|		| Root node.						|
| ProviderLocator 				| 1  		| String	| Booking ID in the Supplier´s system					|
| PropertyReservationNumber 				| 0..1  		| String	| Booking Number in the property´s system (see Metadata method in order to verify if a supplier implements it).	|
| ResStatus					| 1  		| String	| reservation status  (OK = confirmed, RQ = on request, CN = cancelled, UN = unknown.)	|
| Price  					| 0..1     	|		| Total price of this reservation (see [MetaData](/connectiontypessellers/hotelpullsellers/methods/staticcontent/metadata/) in order to verify if a supplier implements it).				|
| @currency					| 1  		| String	| Currency code.					|
| @amount					| 1  		| Decimal	| Book Amount.						|
| @binding					| 1  		| Boolean	| Identifies if is the price is binding (when true the sale price returned **must** not be less than the price informed. |
| @commission					| 1  		| Decimal	| Commission (-1 = not specified, 0 = net price, X = % of the commission that applies to the amount.	|
| Remarks					| 0..1		| String	| Any remarks about this reservation			|
| BillingSupplierCode				| 0..1		| String	| Supplier's billing code. Will be returned if the supplier has different billing accounts and this is informed in the reservation (see [MetaData](/connectiontypessellers/hotelpullsellers/methods/staticcontent/metadata/) in order to verify if a supplier implements it).	|
| Payable					| 0..1     	|		| Payable.						|
| @value					| 1       	|		| Informs Payable.					|
  


### Detailed description

**PreferenceType**: The types that allow, the possible values are:
    - Smoker
    - NonSmoker
    - ExtraBed
    - Cradle
    - DoubleBed
    - TwinBeds
    - ContiguosRooms
    - Wedding
    - LateArrival
    - LateCheckOut
    - EarlyCheckIn
    - GroundFloor
    - TopFlor
    - WithoutVoucher

**ResStatus:**

When making a reservation,  there will be a field named
ResStatus in the response indicating the status of the reservation. It
can have four values: OK, RQ, CN and UN.

-   *OK:* The reservation was completed with no problems.
-   *RQ:* The reservation was completed but the product is still not
    available, so the reservation goes into a waiting list (Request).
-   *CN:* The reservation was completed but due to a supplier error or a timeout
    the system will immediately cancel the reservation to prevent further possible errors.
-   *UN:* The reservation was completed but due to a supplier error or a timeout, the reservation status is unknown.
   It is the client's responsibility to check if the booking is OK.


{{% alert theme="warning" %}}**Important:** be aware that you can receive an error and a reservation status OK in the same response, in this case the booking is confirmed. You should always consider the reservation status returned.{{% /alert %}}


**Note:** *Keep the parameters in the valuation response to include them in the reservation request.*


**Bookings not confirmed:**
Only when the ResStatus = UN and an application error is also returned with type = 303 we can ensure the booking has not been confirmed in the supplier's system. 

~~~xml
<ApplicationError>
    <type>303</type>
    <description>Booking not confirmed</description>
</ApplicationError>
<ResStatus>UN</ResStatus>
~~~

If you receive ResStatus = UN but don't receive a 303 type application error then is the client's responsibility to check if the booking is OK as we can't ensure if the booking is confirmed or not.


**MerchantPay, LaterPay, CardBookingPay & CardCheckInPay**

- PaymentOptions:

- *MerchantPay*: The payment is managed by the supplier.
- *LaterPay*: The payment is managed by the hotel. The customer will use a credit-card as a guarantee for the hotel and the payment
will be completed at check in.
- *CardBookingPay*: The payment is managed by the supplier. The payment is effectuated at the time of booking.
- *CardChekInPay*: The payment is managed by the supplier. The payment is effectuated at check in in the hotel. 


~~~xml
    <PaymentType>MerchantPay</PaymentType>
~~~

If the payment is done by credit card, is it mandatory to specify the payment type and the credit card information in the XML request as in the example below:

~~~xml
    <PaymentType>LaterPay/CardBookingPay/CardCheckInPay</PaymentType>
      <CardInfo>
       <CardCode>XX</CardCode>
       <Number>XXXXXXXXXX</Number>
       <Holder>XXXX</Holder>
       <ValidityDate>   
         <Month>XX</Month>
         <Year>XX</Year>
       </ValidityDate>
       <CVC>XXX</CVC>
     </CardInfo>    
~~~



### DeltaPrice description


**applyBoth:**

Depending on the value of applyBoth:

-   *applyBoth ="false"*: Indicates that one of the conditions (amount
    or percentage) has to meet the criteria before reservation.
-   *applyBoth ="true"*: Indicates that the new price cannot exceed
    the amount or percentage indicated by the client.

An error will be returned if the new price does not abide to *DeltaPrice*. If DeltaPrice tag is not sent and 
the integration implements it, we assume that the price
range is 0 and the process will continue (price is lower
or equal to the price showed in valuation).

This field is implemented if it's native to the supplier or if another availability/valuation request needs to be done in Reservation. In case the supplier blocks the option in valuation, reservation
will be done automatically in reservation method. This information is available in the Static configuration of
each supplier.


### Price difference between the Reservation and Valuation methods

We cannot guarantee that the price will be returned in Reservation, given that this is something which depends on the supplier, and unless they provide us the price in their response, there is no way for us to return it to you.

If the price returned in Reservation method is different than the one returned in the Valuation method, 4 cases could occur. Below, we have explained each of these cases and what should be done if either of them occur:

**Case 1:**

The price in Reservation is lower than the price in Valuation. The selling price for the final customer will be the one in valuation, as this is the one that will be accepted by them at the time of booking. The final price that you should pay the supplier will be the price in Reservation.

**Case 2:**

The price in Reservation is higher than the price in valuation:

**Case 2.1:**

The supplier allows DeltaPrice and you allow a price change of, for example, up to €10, indicating it in through our DeltaPrice field (explained in the previous section):

Valuation: 
~~~xml 
<Price currency = "EUR" amount = "110" binding = "false" commission = "0"/>
~~~

Reservation: 
~~~xml 
<Price currency = "EUR" amount = "110" binding = "false" commission = "0"/>
~~~

When making reservation, you must pay the supplier €110, given that you have decided not to lose the booking even though the price has increased with €10 compared to Valuation.

**Case 2.2:**

The supplier allows DeltaPrice and you DO NOT allow price change. In this case we will return an error, as you do not permit a higher reservation price than the one already established in Valuation.

**Case 2.3:**

The supplier DOES NOT allow DeltaPrice. If the supplier returns a higher price in Reservation than he does in Valuation, then the difference should be reported, as you have not specified in any way that the price can be changed. In this case the supplier has to cover the price change.
