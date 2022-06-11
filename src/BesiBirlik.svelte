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
  let alisKariBbirlik = 0;
  let satisKariBbirlik = 0;
  let satisMilyemBbirlik = 33.5;
  let alisMilyemBbirlik = 33.0;
  let alisYuvarlamaBbirlik = 0;
  let satisYuvarlamaBbirlik = 0;

  const toggle = () => (open = !open);
  function increaseSatisMilyem() {
    satisMilyemBbirlik = Math.round((satisMilyemBbirlik + 0.005) * 1000) / 1000;
  }
  function decreaseSatisMilyem() {
    satisMilyemBbirlik = Math.round((satisMilyemBbirlik - 0.005) * 1000) / 1000;
  }
  function increaseAlisMilyem() {
    alisMilyemBbirlik = Math.round((alisMilyemBbirlik + 0.005) * 1000) / 1000;
  }
  function decreaseAlisMilyem() {
    alisMilyemBbirlik = Math.round((alisMilyemBbirlik - 0.005) * 1000) / 1000;
  }
  function increaseAlisKari() {
    alisKariBbirlik += 50;
  }
  function decreaseAlisKari() {
    alisKariBbirlik -= 50;
  }
  function increaseSatisKari() {
    satisKariBbirlik += 50;
  }
  function decreaseSatisKari() {
    satisKariBbirlik -= 50;
  }
  function increaseAlisYuvarlama() {
    alisYuvarlamaBbirlik += 50;
    alisKariBbirlik += 1;
    alisKariBbirlik -= 1;
  }
  function decreaseAlisYuvarlama() {
    alisYuvarlamaBbirlik -= 50;
    alisKariBbirlik += 1;
    alisKariBbirlik -= 1;
  }
  function increaseSatisYuvarlama() {
    satisYuvarlamaBbirlik += 50;
    satisKariBbirlik += 1;
    satisKariBbirlik -= 1;
  }
  function decreaseSatisYuvarlama() {
    satisYuvarlamaBbirlik -= 50;
    satisKariBbirlik += 1;
    satisKariBbirlik -= 1;
  }
  function adjustBbirlikAlis(num) {
    if (alisYuvarlamaBbirlik !== 0) {
      return roundDown(num, alisYuvarlamaBbirlik);
    } else {
      return parseInt(num);
    }
  }
  function adjustBbirlikSatis(num) {
    if (satisYuvarlamaBbirlik !== 0) {
      return roundUp(num, satisYuvarlamaBbirlik);
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
          >Beşi Biryerde: <Badge>Alış:</Badge>
          {adjustBbirlikAlis($alis * alisMilyemBbirlik - alisKariBbirlik)}
          <Badge>Satış:</Badge>
          {adjustBbirlikSatis(
            $satis * satisMilyemBbirlik + satisKariBbirlik
          )}</span
        >
      </Card></Col
    >
    <div>
      <Button color="danger" on:click="{toggle}">Beşi Biryerde Ayarları</Button>
      <Modal isOpen="{open}" toggle="{toggle}">
        <ModalHeader toggle="{toggle}">Beşi Biryerde Ayarları</ModalHeader>
        <ModalBody>
          <Col sm="auto"
            ><Card body class="mb-3"
              ><span
                ><Button color="danger" on:click="{decreaseSatisMilyem}"
                  >-</Button
                > Toptancıdan Gelişi:
                {satisMilyemBbirlik}
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
                {alisMilyemBbirlik}
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
                {alisKariBbirlik} TL
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
                {satisKariBbirlik} TL
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
                {alisYuvarlamaBbirlik} TL
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
                {satisYuvarlamaBbirlik} TL
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
