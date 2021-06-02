# Strobbo integration APIs

All APIs are built as a restful API which expect to receive data in JSON format accompanied with the correct Header information. Not only the data, but also the header information may differ between the different APIs! Please read the documentation carefully to make sure you are using the correct headers. If you have doubts or questions, you can contact the onlinewerkrooster.be support team (support@strobbo.com).

You can use tools as Insomnia (https://insomnia.rest/) or Postman(https://www.getpostman.com/) in order to test the API, but it is also possible to test the endpoints via the swagger documentation available on https://services.strobbo.com/api/documentation.

## (Technical) Documentation

All details about the available endpoints are documented on https://services.strobbo.com/api/documentation.

![image-20210517115006636](../owr-general/assets/image-20210517115006636.png)

## Deprecated APIs

We still support some older versions of particular API to make sure existing integration still work. Please do **not** use these endpoints for **new** integrations.

| Domain            | Documentation Link                                | Remarks                                                      |
| ----------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| Time registration | [ETC Timeclock API](OwrApiETCTimeclock.md)        | ETC Timeclock integration                                    |
|                   | [ClockTime](OwrApiClockTime.md)                   | New version: https://services.strobbo.com/api/documentation/#/Time%20registration/post_clock |
|                   | [ClockTimeSpecified](OwrApiClockTimeSpecified.md) | New version: https://services.strobbo.com/api/documentation/#/Time%20registration/post_clock |
| Revenue           | [Revenue](OWRAPIRevenue.md)                       | New version: https://services.strobbo.com/api/documentation/#/Revenue |




  ​

