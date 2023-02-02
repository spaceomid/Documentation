!!! Structure info
    ``` json
        // JSON
        {
            "validationMessage": [{"stateCode":200,"message":""}]
            "result": "AnyType",
            "resultStatus": true
        }
    ```
    ``` C#
        // C# code
        public class APIResult<T>
        {
            public EResultStatus ResultStatus { get; set; } = EResultStatus.SUCCESS;

            public T? Result { get; set; }

            public List<APIResultMessage> APIResultMessages { get; set; } = new() { };
        }

        public class APIResultMessage
        {
            public int StateCode { get; set; } = 400;
            public string Message { get; set; } = string.Empty;
        }

        public enum EResultStatus
        {
            SUCCESS,
            FAILED
        }
    ```