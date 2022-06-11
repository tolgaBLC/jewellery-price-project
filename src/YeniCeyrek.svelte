<script>
  import {
    Styles,
    Badge,
    Col,
    Row,
    Card,
    Button,
    Modal,
    ModalBody,
    ModalFooter,
    ModalHeader,
  } from "sveltestrap";
  import { alis } from "./stores.js";
  import { satis } from "./stores.js";
  let open = false;
  let alisKariYenCey = 0;
  let satisKariYenCey = 0;
  let satisMilyemYenCey = 1.63;
  let alisMilyemYenCey = 1.6;
  let alisYuvarlamaYenCey = 0;
  let satisYuvarlamaYenCey = 0;

  const toggle = () => (open = !open);
  function increaseSatisMilyem() {
    satisMilyemYenCey = Math.round((satisMilyemYenCey + 0.005) * 1000) / 1000;
  }
  function decreaseSatisMilyem() {
    satisMilyemYenCey = Math.round((satisMilyemYenCey - 0.005) * 1000) / 1000;
  }
  function increaseAlisMilyem() {
    alisMilyemYenCey = Math.round((alisMilyemYenCey + 0.005) * 1000) / 1000;
  }
  function decreaseAlisMilyem() {
    alisMilyemYenCey = Math.round((alisMilyemYenCey - 0.005) * 1000) / 1000;
  }
  function increaseAlisKari() {
    alisKariYenCey += 1;
  }
  function decreaseAlisKari() {
    alisKariYenCey -= 1;
  }
  function increaseSatisKari() {
    satisKariYenCey += 1;
  }
  function decreaseSatisKari() {
    satisKariYenCey -= 1;
  }
  function increaseAlisYuvarlama() {
    alisYuvarlamaYenCey += 5;
    alisKariYenCey += 1;
    alisKariYenCey -= 1;
  }
  function decreaseAlisYuvarlama() {
    alisYuvarlamaYenCey -= 5;
    alisKariYenCey += 1;
    alisKariYenCey -= 1;
  }
  function increaseSatisYuvarlama() {
    satisYuvarlamaYenCey += 5;
    satisKariYenCey += 1;
    satisKariYenCey -= 1;
  }
  function decreaseSatisYuvarlama() {
    satisYuvarlamaYenCey -= 5;
    satisKariYenCey += 1;
    satisKariYenCey -= 1;
  }
  function adjustCeyrekAlis(num) {
    if (alisYuvarlamaYenCey !== 0) {
      return roundDown(num, alisYuvarlamaYenCey);
    } else {
      return parseInt(num);
    }
  }
  function adjustCeyrekSatis(num) {
    if (satisYuvarlamaYenCey !== 0) {
      return roundUp(num, satisYuvarlamaYenCey);
    } else {
      return parseInt(num);
    }
  }
  function roundDown(num, rNum) {
    return Math.floor(num / rNum) * rNum;
  }
  function roundUp(num, rNum) {
    return Math.ceil(num / rNum) * rNum;
  }
</script>

<Styles />
<Card body color="dark">
  <Row>
    <Col sm="5"
      ><Card body color="warning" class="mb-3"
        ><span
          >Yeni Çeyrek: <Badge>Alış:</Badge>
          {adjustCeyrekAlis($alis * alisMilyemYenCey - alisKariYenCey)}
          <Badge>Satış:</Badge>
          {adjustCeyrekSatis(
            $satis * satisMilyemYenCey + satisKariYenCey
          )}</span
        >
      </Card></Col
    >
    <div>
      <Button color="danger" on:click="{toggle}">Yeni Çeyrek Ayarları</Button>
      <Modal isOpen="{open}" toggle="{toggle}">
        <ModalHeader toggle="{toggle}">Yen Çeyrek Ayarlar</ModalHeader>
        <ModalBody>
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisMilyem}"
                  >-</Button
                > Toptancıdan Gelişi:
                {satisMilyemYenCey}
                <Button color="success " on:click="{increaseSatisMilyem}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseAlisMilyem}"
                  >-</Button
                > Toptancının Alışı:
                {alisMilyemYenCey}
                <Button color="success " on:click="{increaseAlisMilyem}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseAlisKari}">-</Button>

                Alış Karı:
                {alisKariYenCey} TL
                <Button color="success " on:click="{increaseAlisKari}">+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisKari}">-</Button
                >

                Satış Karı:
                {satisKariYenCey} TL
                <Button color="success " on:click="{increaseSatisKari}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseAlisYuvarlama}"
                  >-</Button
                >

                Alış Yuvarlama:
                {alisYuvarlamaYenCey} TL
                <Button color="success " on:click="{increaseAlisYuvarlama}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisYuvarlama}"
                  >-</Button
                >

                Satış Yuvarlama:
                {satisYuvarlamaYenCey} TL
                <Button color="success " on:click="{increaseSatisYuvarlama}"
                  >+</Button
                ></span
              ></Card
            ></Col
          >
        </ModalBody>
        <ModalFooter>
          <!-- <Button color="primary" on:click="{toggle}">Kaydet</Button> -->
          <Button color="secondary" on:click="{toggle}">Kapat</Button>
        </ModalFooter>
      </Modal>
    </div>
  </Row>
</Card>

<style>
  span {
    font-weight: bold;
    display: inline-block;
    /* font-size: 1.4em;
      background: linear-gradient(to right, black 90%, white 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent; */
  }
</style>
