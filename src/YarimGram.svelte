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
  let alisKariYrmGr = 0;
  let satisKariYrmGr = 0;
  let satisMilyemYrmGr = 0.945;
  let alisMilyemYrmGr = 0.912;
  let alisYuvarlamaYrmGr = 0;
  let satisYuvarlamaYrmGr = 0;

  const toggle = () => (open = !open);
  function increaseSatisMilyem() {
    satisMilyemYrmGr = Math.round((satisMilyemYrmGr + 0.001) * 1000) / 1000;
  }
  function decreaseSatisMilyem() {
    satisMilyemYrmGr = Math.round((satisMilyemYrmGr - 0.001) * 1000) / 1000;
  }
  function increaseAlisMilyem() {
    alisMilyemYrmGr = Math.round((alisMilyemYrmGr + 0.001) * 1000) / 1000;
  }
  function decreaseAlisMilyem() {
    alisMilyemYrmGr = Math.round((alisMilyemYrmGr - 0.001) * 1000) / 1000;
  }
  function increaseAlisKari() {
    alisKariYrmGr += 1;
  }
  function decreaseAlisKari() {
    alisKariYrmGr -= 1;
  }
  function increaseSatisKari() {
    satisKariYrmGr += 1;
  }
  function decreaseSatisKari() {
    satisKariYrmGr -= 1;
  }
  function increaseAlisYuvarlama() {
    alisYuvarlamaYrmGr += 5;
    alisKariYrmGr += 1;
    alisKariYrmGr -= 1;
  }
  function decreaseAlisYuvarlama() {
    alisYuvarlamaYrmGr -= 5;
    alisKariYrmGr += 1;
    alisKariYrmGr -= 1;
  }
  function increaseSatisYuvarlama() {
    satisYuvarlamaYrmGr += 5;
    satisKariYrmGr += 1;
    satisKariYrmGr -= 1;
  }
  function decreaseSatisYuvarlama() {
    satisYuvarlamaYrmGr -= 5;
    satisKariYrmGr += 1;
    satisKariYrmGr -= 1;
  }
  function adjustYrmGrAlis(num) {
    if (alisYuvarlamaYrmGr !== 0) {
      return roundDown(num, alisYuvarlamaYrmGr);
    } else {
      return parseInt(num);
    }
  }
  function adjustYrmGrSatis(num) {
    if (satisYuvarlamaYrmGr !== 0) {
      return roundUp(num, satisYuvarlamaYrmGr);
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
          >0.5 Gram 22k: <Badge>Alış:</Badge>
          {adjustYrmGrAlis(($alis * alisMilyemYrmGr) / 2 - alisKariYrmGr)}
          <Badge>Satış:</Badge>
          {adjustYrmGrSatis(
            ($satis * satisMilyemYrmGr) / 2 + satisKariYrmGr
          )}</span
        >
      </Card></Col
    >
    <div>
      <Button color="danger" on:click="{toggle}">0.5 Gram 22k Ayarları</Button>
      <Modal isOpen="{open}" toggle="{toggle}">
        <ModalHeader toggle="{toggle}">0.5 Gram 22k Ayarları</ModalHeader>
        <ModalBody>
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisMilyem}"
                  >-</Button
                > Toptancıdan Gelişi:
                {satisMilyemYrmGr}
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
                {alisMilyemYrmGr}
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
                {alisKariYrmGr} TL
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
                {satisKariYrmGr} TL
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
                {alisYuvarlamaYrmGr} TL
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
                {satisYuvarlamaYrmGr} TL
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
