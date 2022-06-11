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
  let alisKariEsCey = 0;
  let satisKariEsCey = 0;
  let satisMilyemEsCey = 1.61;
  let alisMilyemEsCey = 1.6;
  let alisYuvarlamaEsCey = 0;
  let satisYuvarlamaEsCey = 0;

  const toggle = () => (open = !open);
  function increaseSatisMilyem() {
    satisMilyemEsCey = Math.round((satisMilyemEsCey + 0.005) * 1000) / 1000;
  }
  function decreaseSatisMilyem() {
    satisMilyemEsCey = Math.round((satisMilyemEsCey - 0.005) * 1000) / 1000;
  }
  function increaseAlisMilyem() {
    alisMilyemEsCey = Math.round((alisMilyemEsCey + 0.005) * 1000) / 1000;
  }
  function decreaseAlisMilyem() {
    alisMilyemEsCey = Math.round((alisMilyemEsCey - 0.005) * 1000) / 1000;
  }
  function increaseAlisKari() {
    alisKariEsCey += 1;
  }
  function decreaseAlisKari() {
    alisKariEsCey -= 1;
  }
  function increaseSatisKari() {
    satisKariEsCey += 1;
  }
  function decreaseSatisKari() {
    satisKariEsCey -= 1;
  }
  function increaseAlisYuvarlama() {
    alisYuvarlamaEsCey += 5;
    alisKariEsCey += 1;
    alisKariEsCey -= 1;
  }
  function decreaseAlisYuvarlama() {
    alisYuvarlamaEsCey -= 5;
    alisKariEsCey += 1;
    alisKariEsCey -= 1;
  }
  function increaseSatisYuvarlama() {
    satisYuvarlamaEsCey += 5;
    satisKariEsCey += 1;
    satisKariEsCey -= 1;
  }
  function decreaseSatisYuvarlama() {
    satisYuvarlamaEsCey -= 5;
    satisKariEsCey += 1;
    satisKariEsCey -= 1;
  }
  function adjustCeyrekAlis(num) {
    if (alisYuvarlamaEsCey !== 0) {
      return roundDown(num, alisYuvarlamaEsCey);
    } else {
      return parseInt(num);
    }
  }
  function adjustCeyrekSatis(num) {
    if (satisYuvarlamaEsCey !== 0) {
      return roundUp(num, satisYuvarlamaEsCey);
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
          >Eski Çeyrek: <Badge>Alış:</Badge>
          {adjustCeyrekAlis($alis * alisMilyemEsCey - alisKariEsCey)}
          <Badge>Satış:</Badge>
          {adjustCeyrekSatis($satis * satisMilyemEsCey + satisKariEsCey)}</span
        >
      </Card></Col
    >
    <div>
      <Button color="danger" on:click="{toggle}">Eski Çeyrek Ayarları</Button>
      <Modal isOpen="{open}" toggle="{toggle}">
        <ModalHeader toggle="{toggle}">Eski Çeyrek Ayarları</ModalHeader>
        <ModalBody>
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisMilyem}"
                  >-</Button
                > Toptancıdan Gelişi:
                {satisMilyemEsCey}
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
                {alisMilyemEsCey}
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
                {alisKariEsCey} TL
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
                {satisKariEsCey} TL
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
                {alisYuvarlamaEsCey} TL
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
                {satisYuvarlamaEsCey} TL
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
