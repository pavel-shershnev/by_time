<template>

<div id="map" style="width: 900px; height: 700px"></div>

</template>

<script>

export default {
data() {
  return {
  }
},
mounted() {
  ymaps.ready(function () {
    var geolocation = ymaps.geolocation,
      myMap = new ymaps.Map('map', {
        center: [59.9386, 30.3141],
        zoom: 12,
        controls: ['routeButtonControl', 'zoomControl', 'geolocationControl']
    },{
        suppressMapOpenBlock: true
    });
    // ==============================геолокация
     geolocation.get({
        provider: 'browser',
        mapStateAutoApply: true,
    }).then(function (result) {
        // Добавление геолокации. Если браузер не поддерживает эту функциональность, метка не будет добавлена на карту.
        result.geoObjects.options.set('preset', 'islands#geolocationIcon');
        myMap.geoObjects.add(result.geoObjects);
    });
    myMap.geoObjects
        .add(new ymaps.Placemark([59.907978, 30.514729], {
            balloonContent: '<strong>Шаверма ЕвроКебаб</strong>'
        }, {
            preset: 'islands#icon',
            iconColor: '#0095b6'
        }))
        .add(new ymaps.Placemark([59.906199, 30.521479], {
            balloonContent: '<img src="https://avatars.mds.yandex.net/get-altay/1588111/2a0000016c1fdacffdfb565160e15585c2cf/XXXL" alt="" style="max-width: 100px; max-height:100px"><strong>Кафе солнышко</strong><div><button style="background-color: aquamarine;">заказ онлайн</button></div>'
        }, {
            preset: 'islands#icon',
            iconColor: '#0095b6'
        }))





    // ==============================маршруты до объектов
    var control = myMap.controls.get('routeButtonControl');
    // Зададим координаты пункта отправления с помощью геолокации.
    control.routePanel.geolocate('from');
    // Откроем панель для построения маршрутов.
    control.state.set('expanded', false);
    // ===================================================
});
},
}
</script>
 <style>
      html, body, #map {
          width: 100%; height: 100%; padding: 0; margin: 0;
      }
  </style>
