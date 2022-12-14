# Basic Fuzzing (OWASP Top 10 - Identification and Authentication Failures.docx)

1. Complete Basic Spidering

2. Look for a `POST Request` that takes in a username and password field

3. Select to view the `REQUEST`

4. Highlight the payload field to Fuzz

5. Right click and select `Fuzz`

6. Configure and add the Payload with the following wordlists for the correct fields

    - Username

            File Fuzzers > fuzzdb > wordlists-user-passwd > generic-listpairs > http_default_users.txt

    - Password

            File Fuzzers > fuzzdb > wordlists-user-passwd > generic-listpairs > http_default_pass.txt

7. Click `Message Processors` in the Fuzzer top pane

8. Configure a new `Tag Creator`

9. Match the Regex to the one found on the site on invalid login

10. Place a `Tag` value of `Failed`

11. Select the `Tag Creator` and click the `Top` button

12. Click `Start Fuzzer`

13. Filter the result by clicking the `State`

14. The state that does not state Failed is a successful fuzz