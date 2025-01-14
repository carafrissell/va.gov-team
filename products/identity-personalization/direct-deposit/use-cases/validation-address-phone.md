# Direct deposit for compensation and pension: user doesn't have a valid mailing address or phone number in their profile

**Last updated June 27, 2022**

If an LOA3 user attempts to update their compensation and pension direct deposit information (DD), and they don't have a valid mailing address or home or work number on file, they're blocked from making an update and prompted to review their contact information. There is no actual requirement for a user to have a valid address and phone to update direct deposit data; this requirement is a symptom of the BGS service that updates direct deposit and how functionality used to work when the ability to update direct deposit existed on eBenefits.

In June 2022, the DD team started working with the BGS team to remove contact information from this service. That work is currently in progress.

**Note:** This does not apply to education direct deposit information.

## UX
- If a user doesn't have a valid phone number (home or work) or mailing address in their profile, and they attempt to update their DD information, they will see an error message at the top of the DD form.
- Uses the [error alert component](https://design.va.gov/components/alert#error-alert) from the VA design system
- [Desktop mock-up](https://www.sketch.com/s/1a920e73-1dcb-47c4-aae8-08656756c131/a/ELA5LMg)
- [Mobile mock-up](https://www.sketch.com/s/1a920e73-1dcb-47c4-aae8-08656756c131/a/jg1WgEa)

## Technical information
- The BGS service that updates DD was designed to also update address and phone at the same time. So before adding or updating DD, the Personal Payment Information Update (PPIU) API calls BGS to get current address, phone and EFT. Then it modifies the Electronic Fund Transfer (EFT) account info and sends it along with the original address and phone data back to BGS. If their validation fails due to missing data, the EFT update will fail even though that part of the request is correct. 
- If the user has a invalid phone/address, we are getting back an error message with the generic error key `cnp.payment.generic.error.message`  and we are determining if the error is phone/address related by looking for the `message.text` to include error text like `address update` `night phone number` `day phone number` etc to determine what is invalid
- `night phone`  and `night area number` align with `home phone`  
- `day phone number` and `day area number` align with `work phone`
- We are mostly certain a user needs to have a valid mailing address, home phone number, and work phone number to successfully update direct depositinformation. 

## Codes
TBD

## How to reproduce

- This error can be reproduced locally (not on staging)
