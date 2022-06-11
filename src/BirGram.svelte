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
  let alisKariBirGr = 0;
  let satisKariBirGr = 0;
  let satisMilyemBirGr = 0.93;
  let alisMilyemBirGr = 0.912;
  let alisYuvarlamaBirGr = 0;
  let satisYuvarlamaBirGr = 0;

  const toggle = () => (open = !open);
  function increaseSatisMilyem() {
    satisMilyemBirGr = Math.round((satisMilyemBirGr + 0.001) * 1000) / 1000;
  }
  function decreaseSatisMilyem() {
    satisMilyemBirGr = Math.round((satisMilyemBirGr - 0.001) * 1000) / 1000;
  }
  function increaseAlisMilyem() {
    alisMilyemBirGr = Math.round((alisMilyemBirGr + 0.001) * 1000) / 1000;
  }
  function decreaseAlisMilyem() {
    alisMilyemBirGr = Math.round((alisMilyemBirGr - 0.001) * 1000) / 1000;
  }
  function increaseAlisKari() {
    alisKariBirGr += 1;
  }
  function decreaseAlisKari() {
    alisKariBirGr -= 1;
  }
  function increaseSatisKari() {
    satisKariBirGr += 1;
  }
  function decreaseSatisKari() {
    satisKariBirGr -= 1;
  }
  function increaseAlisYuvarlama() {
    alisYuvarlamaBirGr += 5;
    alisKariBirGr += 1;
    alisKariBirGr -= 1;
  }
  function decreaseAlisYuvarlama() {
    alisYuvarlamaBirGr -= 5;
    alisKariBirGr += 1;
    alisKariBirGr -= 1;
  }
  function increaseSatisYuvarlama() {
    satisYuvarlamaBirGr += 5;
    satisKariBirGr += 1;
    satisKariBirGr -= 1;
  }
  function decreaseSatisYuvarlama() {
    satisYuvarlamaBirGr -= 5;
    satisKariBirGr += 1;
    satisKariBirGr -= 1;
  }
  function adjustBirGramAlis(num) {
    if (alisYuvarlamaBirGr !== 0) {
      return roundDown(num, alisYuvarlamaBirGr);
    } else {
      return parseInt(num);
    }
  }
  function adjustBirGramSatis(num) {
    if (satisYuvarlamaBirGr !== 0) {
      return roundUp(num, satisYuvarlamaBirGr);
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
          >1 Gram 22k: <Badge>Alış:</Badge>
          {adjustBirGramAlis($alis * alisMilyemBirGr - alisKariBirGr)}
          <Badge>Satış:</Badge>
          {adjustBirGramSatis($satis * satisMilyemBirGr + satisKariBirGr)}</span
        >
      </Card></Col
    >
    <div>
      <Button color="danger" on:click="{toggle}">1 Gram 22k Ayarları</Button>
      <Modal isOpen="{open}" toggle="{toggle}">
        <ModalHeader toggle="{toggle}">1 Gram 22k Ayarları</ModalHeader>
        <ModalBody>
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisMilyem}"
                  >-</Button
                > Toptancıdan Gelişi:
                {satisMilyemBirGr}
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
                {alisMilyemBirGr}
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
                {alisKariBirGr} TL
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
                {satisKariBirGr} TL
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
                {alisYuvarlamaBirGr} TL
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
                {satisYuvarlamaBirGr} TL
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
