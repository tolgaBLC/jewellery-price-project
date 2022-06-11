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
  let alisKariCyrkGr = 0;
  let satisKariCyrkGr = 0;
  let satisMilyemCyrkGr = 0.95;
  let alisMilyemCyrkGr = 0.912;
  let alisYuvarlamaCyrkGr = 0;
  let satisYuvarlamaCyrkGr = 0;

  const toggle = () => (open = !open);
  function increaseSatisMilyem() {
    satisMilyemCyrkGr = Math.round((satisMilyemCyrkGr + 0.001) * 1000) / 1000;
  }
  function decreaseSatisMilyem() {
    satisMilyemCyrkGr = Math.round((satisMilyemCyrkGr - 0.001) * 1000) / 1000;
  }
  function increaseAlisMilyem() {
    alisMilyemCyrkGr = Math.round((alisMilyemCyrkGr + 0.001) * 1000) / 1000;
  }
  function decreaseAlisMilyem() {
    alisMilyemCyrkGr = Math.round((alisMilyemCyrkGr - 0.001) * 1000) / 1000;
  }
  function increaseAlisKari() {
    alisKariCyrkGr += 1;
  }
  function decreaseAlisKari() {
    alisKariCyrkGr -= 1;
  }
  function increaseSatisKari() {
    satisKariCyrkGr += 1;
  }
  function decreaseSatisKari() {
    satisKariCyrkGr -= 1;
  }
  function increaseAlisYuvarlama() {
    alisYuvarlamaCyrkGr += 5;
    alisKariCyrkGr += 1;
    alisKariCyrkGr -= 1;
  }
  function decreaseAlisYuvarlama() {
    alisYuvarlamaCyrkGr -= 5;
    alisKariCyrkGr += 1;
    alisKariCyrkGr -= 1;
  }
  function increaseSatisYuvarlama() {
    satisYuvarlamaCyrkGr += 5;
    satisKariCyrkGr += 1;
    satisKariCyrkGr -= 1;
  }
  function decreaseSatisYuvarlama() {
    satisYuvarlamaCyrkGr -= 5;
    satisKariCyrkGr += 1;
    satisKariCyrkGr -= 1;
  }
  function adjustCyrkGrAlis(num) {
    if (alisYuvarlamaCyrkGr !== 0) {
      return roundDown(num, alisYuvarlamaCyrkGr);
    } else {
      return parseInt(num);
    }
  }
  function adjustCyrkGrSatis(num) {
    if (satisYuvarlamaCyrkGr !== 0) {
      return roundUp(num, satisYuvarlamaCyrkGr);
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
          >0.25 Gram 22k: <Badge>Alış:</Badge>
          {adjustCyrkGrAlis(($alis * alisMilyemCyrkGr) / 4 - alisKariCyrkGr)}
          <Badge>Satış:</Badge>
          {adjustCyrkGrSatis(
            ($satis * satisMilyemCyrkGr) / 4 + satisKariCyrkGr
          )}</span
        >
      </Card></Col
    >
    <div>
      <Button color="danger" on:click="{toggle}">0.25 Gram 22k Ayarları</Button>
      <Modal isOpen="{open}" toggle="{toggle}">
        <ModalHeader toggle="{toggle}">0.25 Gram 22k Ayarları</ModalHeader>
        <ModalBody>
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisMilyem}"
                  >-</Button
                > Toptancıdan Gelişi:
                {satisMilyemCyrkGr}
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
                {alisMilyemCyrkGr}
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
                {alisKariCyrkGr} TL
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
                {satisKariCyrkGr} TL
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
                {alisYuvarlamaCyrkGr} TL
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
                {satisYuvarlamaCyrkGr} TL
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
