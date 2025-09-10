# BR-UTM Observer

* No arquivo [flight_data.py](./backend/mock/flight_data.py) temos dados de voo para testes
* Em [fetch.py](./backend/routes/fetch.py) podemos remover os comentários (abaixo) para termos dados voo simulados:

    ```python
    async def query_flights(
            area: QueryFlightsRequest
    ):
        flights_service = FlightsService()

        res = await flights_service.query_flights(area)
        # res.flights += generate_flight_mock_data()
        # res = QueryFlightsResponse(
        #     flights=generate_flight_mock_data(),
        #     partial=False,
        #     errors=[],
        #     timestamp=Time(
        #         value=datetime.now(),
        #         format=TimeFormat.RFC3339,
        #     )
        # )

        return Response(
            message="Live flight data requested",
            data=res,
        )
    ```

* Isto no entanto ainda não é o suficiente para observar todas as funcionalidades do aplicativo
* Aparentemente é necessária uma chave válida para o serviço `http://api.dev.br-utm.org` e `brutm` (que estamos usando) e assumimos que parece não ser (ver `.env`):

    ```ini
    BRUTM_KEY=brutm
    BRUTM_BASE_URL=http://api.dev.br-utm.org
    ```

* Outra explicação é q os dados em [flight_data.py](./backend/mock/flight_data.py) são inconsistentes com o que está disponível em [http://api.dev.br-utm.org](http://api.dev.br-utm.org)
* Por exemplo, dos logs:

    ```
    === Requesting Identification Service Area Details ===
    Area ID: 00000000-0000-4000-8000-000000000002
    Base URL: http://172.18.35.75:8847/
    Endpoint: /uss/identification_service_areas/00000000-0000-4000-8000-000000000002
    Trying to get token for audience:             172.18.35.75 and scope: RIDAuthority.DISPLAY_PROVIDER
    Error querying flights for ISA: http://172.18.35.75:8847/ 500: {'message': 'Request error occurred.', 'data': ''}
    500: {'message': 'Request error occurred.', 'data': ''}
    Error fetching service area details: 00000000-0000-4000-8000-000000000002
    {'operational_intents': [], 'constraints': [], 'identification_service_areas': []}
    ```


