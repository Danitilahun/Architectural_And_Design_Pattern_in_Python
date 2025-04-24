# Designing Good APIs

This explanation focuses on the principles of good API design, covering API definition, HTTP endpoints, common pitfalls, and considerations for performance and scalability.

## 1. API Definition

*   An API is a documented way for external consumers to interact with your code.
*   API describes how interact with your code, but not how your code works.
It is a contract to state what something will do.
*It just a way they can interact with your code*

## 2. Example: GetAdmins API

*   **Use Case:** Finding all admins in a WhatsApp group.
*   **API Definition:**
    *   Function Name: `GetAdmins`
    *   Parameter: `groupID` (string)
    *   Errors:
        *   `groupID` does not exist.
        *   Group is deleted (optional, depending on logic).
    *   Response:
        *   `admins` (list of Admin objects). Admin object might have name, user ID etc.
*What should it do?*

## 3. API Design Checklist

*   **Where does it belong?** (Microservice architecture) This question can asked itself.
    *   If you have the service that controls the users, if the API pertains to that, then it should have control of the API
*What is it that I need to passed through ( The Group ID)*

## 4. Common API Design Mistakes

*   **Naming:** If it's `getAdmins`, it should *only* return admins.
*   **Unnecessary Parameters:** Don't add parameters unless absolutely necessary.  Avoid checking if data being passed in to use is valid

## 5. API Optimization

*   Additional parameters can be acceptable for optimization purposes (e.g., providing more information to reduce the number of calls to other services). But it has to change with the action
*   **Response Stuffing:** Avoid stuffing the response with extra information in anticipation of future requests. If the users doesn't needed to do so change it, do it.

## 6. HTTP Endpoints

*   **Address:** `site/model/function`
*   **Example:**
    *`address=site/group/getAdmins/V1`
*What is it that I did?*
*   **Method:** `POST` (with group ID as a JSON object in the request body).
    *This also includes the HTTP requests and browsers*
*   **Response:** JSON array of admins with ID and name.

## 7. GET vs. POST

*   Can it be done using a `GET` request?
    *Absolutely. The users might also have the function to get it to
*   Avoid mixing routing with action (e.g., don't put the action as a parameter in the request body).
* So you can make it short by make this request a GET to the server by using this request.
*Make sure for HTTP verbs (get)

## 8. Side Effects

*What happened if one admin is not on the service list?*
*What should the system do?"
*It does too much.
*   APIs should have no side effects. A lots of flags for single API should be broken into multiple API's

*   Doing multiple things in one function.
*   Lack of atomicity (if the operation fails partway through, what happens?).

## 9. Response Size

*   If the response is very large (e.g., 200 members with detailed profiles), break it into pieces:
    *   **Pagination:** Client is responsible for requesting data in chunks (first 10, then next 10, etc.).
    *  **Fragmentation:** It has to do with HTTP, its on the internal control *internal protocol are shorter responses*. The data to send by sequence number.
*   This can be done if the response for that API is huge, the more it is, and the more it is to download.

## 10. Consistency

*   **Data Consistency:** How consistent do you want your data
*   **Cache:** Or not a cache?
*Is there a lot of load?
What kind of thing is it?""
*The load on the database might reduce their response.

*   Is perfect consistency required, or is eventual consistency acceptable?
*   Caching can improve performance but introduce eventual consistency.
*   Service degradation:
*Essentials, still
responding, without completely thrashing.*